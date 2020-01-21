# DJIWaypointMissionDocs  

## DJI Waypoint class  
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
*Description:*  
Altitude of the aircraft in meters when it reaches waypoint. The altitude of the aircraft is relative to the ground at the take-off location, has a range of [-200,500], and should not be larger than the aircraft's maximum altitude. If two adjacent waypoints have different altitudes, the altitude will gradually change as the aircraft flys between waypoints.
\
\
property heading
```
@IntRange(from = MIN_HEADING, to = MAX_HEADING) int heading
```
*Description*  
The heading to which the aircraft will rotate by the time it reaches the waypoint. The aircraft heading will gradually change between two waypoints with different headings if the waypoint mission's getHeadingMode is set to USING_WAYPOINT_HEADING. A heading has a range of [-180, 180] degrees, where 0 represents True North.
\
\
property gimbalPitch
```
@FloatRange(from = MIN_GIMBAL_PITCH, to = MAX_GIMBAL_PITCH) float gimbalPitch
```
*Description*  
Gimbal pitch angle when reached this waypoint. This property is used when the isGimbalPitchRotationEnabled is TRUE. Value should in range [-90, 0] degree.
\
\
property speed
```
@FloatRange(from = MIN_SPEED, to = MAX_SPEED) float speed
```
*Description*
The base automatic speed of the aircraft as it moves between this waypoint and the next waypoint with range [0, 15] m/s. By default, it is 0.0 and the aircraft will fly with getAutoFlightSpeed of the waypoint mission. If greater than 0, 'speed' will override getAutoFlightSpeed. This 'speed' can only define movement forward through the waypoint mission in comparison to getAutoFlightSpeed which can be both forward and backwards through a waypoint mission.
Waypoint mission speed priority from highest to lowest is:
1) manual speed adjustment with remote controller joy sticks
2) 'speed'
3) setAutoFlightSpeed
4) getAutoFlightSpeed
