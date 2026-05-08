# Module Imports
from LocoXtreme import Connection
from LocoXtreme import LocoXtreme
from LocoXtreme import MotorDirection as MD
from LocoXtreme import Data
from LocoXtreme import WaitType as WT
from LocoXtreme import Song
from LocoXtreme import Note
import time

# Create Connection Instance
connection = Connection()

# USB Connection Setup
connection.setup()

# Scan for Robots
robots = connection.scan(4000)

# Get Named Robot
robot = connection.get_robot(robots, "pink")

# Create LocoXtreme Object
locoxtreme = LocoXtreme(robot)

# Connect to LocoXtreme
locoxtreme.connect()

# Activate Motors
locoxtreme.activate_motors()

# Enable Sensors
locoxtreme.enable_sensor(Data.ULTRASONIC, 1)

# Pause for Initializations
time.sleep(0.4)

wall_distance = 23

def greenLight():
    locoxtreme.set_lights(0, 255, 0)
    locoxtreme.sync_lights()
def redLight():
    locoxtreme.set_lights(255, 0, 0)
    locoxtreme.sync_lights()

def stopRobot():
    locoxtreme.move(MD.FORWARD, MD.FORWARD, 0, 0, False)

def moveForward():
    greenLight()
    locoxtreme.move(MD.FORWARD, MD.FORWARD, 1.0, 1.0, False)
def backupLittle():
    redLight()
    locoxtreme.move(MD.BACKWARD, MD.BACKWARD, 0.3, 0.3, False)
    stopRobot()

def turnLeft90():
    redLight()
    locoxtreme.setup_wait(WT.ROTATION, 88.5)
    locoxtreme.move(MD.BACKWARD, MD.FORWARD, 1, 1, True)
    stopRobot()
def turnRight180():
    redLight()
    locoxtreme.setup_wait(WT.ROTATION, 178)
    locoxtreme.move(MD.FORWARD, MD.BACKWARD, 1, 1, True)
    stopRobot()


def wallInFront():
    distance = locoxtreme.get_sensor_value(Data.ULTRASONIC)
    return distance < wall_distance


while True:
    moveForward()
    if wallInFront():

        stopRobot()
        redLight()
        turnLeft90()
        time.sleep(0.2)

        if wallInFront():
            backupLittle()
            turnRight180()
            moveForward()

        else:
            moveForward()

    time.sleep(0.01)


# Deactivate Motors
locoxtreme.deactivate_motors()

# Disconnect From LocoXtreme
locoxtreme.disconnect()
