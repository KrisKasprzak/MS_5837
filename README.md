This library is a copy of the work done by Blue Robotics Arduino. The The only chages to their work is
<br>
1. renamed MS... to MS_... to avoid library conflicts
<br>
2. changed read() to be "non-blocking" by eliminating the two delay(20) calls to where read() must be done in loop and if 20ms has passed the first
conversion is made, if another 20 ms has passed the second conversion and caluclations are made. User can then call temperature(), altitude() etc. at any time
and any know data will be returned. The end result is that copnversions are made when ready but not block general program exection. My implementation may not be
the most professional non-blocking method but it suites my use case, an interrupt scheme my be a better way to go.
<br>
The results are speeding getting all readings from 41ms to ~11 us

implementation will require read to ONLY be in a continuous loop 

loop(){
		
	sensor.read();
	
	if (some update time has passed) {
		reset update time
		Serial.println(sensor.pressure());
	}
}
