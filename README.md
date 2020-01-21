# DJIWaypointMissionDocs  
\
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
property heading
```
@IntRange(from = MIN_HEADING, to = MAX_HEADING) int heading
```
*Description*  
The heading to which the aircraft will rotate by the time it reaches the waypoint. The aircraft heading will gradually change between two waypoints with different headings if the waypoint mission's getHeadingMode is set to USING_WAYPOINT_HEADING. A heading has a range of [-180, 180] degrees, where 0 represents True North.
\
property gimbalPitch
```
@FloatRange(from = MIN_GIMBAL_PITCH, to = MAX_GIMBAL_PITCH) float gimbalPitch
```
*Description*  
Gimbal pitch angle when reached this waypoint. This property is used when the isGimbalPitchRotationEnabled is TRUE. Value should in range [-90, 0] degree.
\
