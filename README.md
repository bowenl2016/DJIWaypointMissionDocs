# DJIWaypointMissionDocs  

## DJI Waypoint  
The class represents a target point in the waypoint mission. For a waypoint mission, a flight route consists of multiple Waypoint objects. The user can also define the actions to perform for each Waypoint.
\
constructor method
```
Waypoint(double latitude, double longitude, float altitude)
```
\
property coordinate
```
LocationCoordinate2D coordinate
```
\
property altitude
```
@FloatRange(from = MIN_ALTITUDE, to = MAX_ALTITUDE) float altitude
```
<details>
  <summary>Description:</summary>
  
Altitude of the aircraft in meters when it reaches waypoint. The altitude of the aircraft is relative to the ground at the take-off location, has a range of [-200,500], and should not be larger than the aircraft's maximum altitude. If two adjacent waypoints have different altitudes, the altitude will gradually change as the aircraft flys between waypoints.
</details>

\
property heading
```
@IntRange(from = MIN_HEADING, to = MAX_HEADING) int heading
```
<details>
  <summary>Description:</summary>

The heading to which the aircraft will rotate by the time it reaches the waypoint. The aircraft heading will gradually change between two waypoints with different headings if the waypoint mission's getHeadingMode is set to USING_WAYPOINT_HEADING. A heading has a range of [-180, 180] degrees, where 0 represents True North.
</details>

\
property gimbalPitch
```
@FloatRange(from = MIN_GIMBAL_PITCH, to = MAX_GIMBAL_PITCH) float gimbalPitch
```
<details>
  <summary>Description:</summary>

Gimbal pitch angle when reached this waypoint. This property is used when the isGimbalPitchRotationEnabled is TRUE. Value should in range [-90, 0] degree.
</details>

\
property speed
```
@FloatRange(from = MIN_SPEED, to = MAX_SPEED) float speed
```
<details>
  <summary>Description:</summary>

The base automatic speed of the aircraft as it moves between this waypoint and the next waypoint with range [0, 15] m/s. By default, it is 0.0 and the aircraft will fly with getAutoFlightSpeed of the waypoint mission. If greater than 0, 'speed' will override getAutoFlightSpeed. This 'speed' can only define movement forward through the waypoint mission in comparison to getAutoFlightSpeed which can be both forward and backwards through a waypoint mission.
Waypoint mission speed priority from highest to lowest is:
1) manual speed adjustment with remote controller joy sticks
2) 'speed'
3) setAutoFlightSpeed
4) getAutoFlightSpeed
</details>


## DJI WaypointAction  
<details>
  <summary>Description:</summary>

This class represents a waypoint action for Waypoint. It determines what action is performed when the aircraft reaches the corresponding waypoint.
An action's execution time is at maximum 6 seconds except stay action. If an action is not finished after 6 seconds, this action will be terminated, and the drone will fly to next waypoint.
6 types of actions
- Stay
- ShootPhoto
- StartRecord
- StopRecord
- RotateAircraft
- RotateGimbalPitch
</details>

```
WaypointAction(WaypointActionType actionType, int actionParam)
waypoint.addAction(action)
```
<details>
  <summary>Description:</summary>

Adds a waypoint action to a waypoint. The number of waypoint actions should not be larger than MAX_ACTION_COUNT. The action will only be executed when the mission's getFlightPathMode property is set to NORMAL and will not be executed when the mission's getFlightPathMode property is set to CURVED. The maximum number of waypoint actions you can add is 15.
</details>


## DJI WaypointMission  
<details>
  <summary>Description:</summary>

In the waypoint mission, the aircraft will travel between waypoints, execute actions at waypoints, and adjust heading and altitude between waypoints. Waypoints are physical locations to which the aircraft will fly. Creating a series of waypoints, in effect, will program a flight route for the aircraft to follow. Actions can also be added to waypoints, which will be carried out when the aircraft reaches the waypoint. The aircraft travels between waypoints automatically at a base speed. However, the user can change the speed by using the pitch joystick. If the stick is pushed up, the speed will increase. If the stick is pushed down, the speed will slow down. The stick can be pushed down to stop the aircraft and further pushed to start making the aircraft travel back along the path it came. When the aircraft is traveling through waypoints in the reverse order, it will not execute waypoint actions at each waypoint. If the stick is released, the aircraft will again travel through the waypoints in the original order, and continue to execute waypoint actions (even if executed previously). If the aircraft is pulled back along the waypoint mission all the way to the first waypoint, then it will hover in place until the stick is released enough for it to again progress through the mission from start to finish. It is not supported by Mavic Pro when using WiFi connection. It is not supported by Spark.
</details>

Waypoint Information
- getWaypointCount
- getWaypointList
  
Flight Speed
- getMaxFlightSpeed
- getAutoFlightSpeed
  
Start Mission Behavior
- getGotoFirstWaypointMode

End Mission Behavior
- getFinishedAction
  
Aircraft Heading
- getHeadingMode
- getPointOfInterest
  
Flight Path
- getFlightPathMode
  
## WaypointMissionOperator  
The waypoint operator is the only object that controls, runs and monitors Waypoint Missions. It can be accessed from MissionControl.
