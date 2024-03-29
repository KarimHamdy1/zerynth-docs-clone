# Generic Sensor Library

This module contains class definitions for sensors. The Sensor class provides methods for handling generic sensors connected to specific pins of a device. It also provides easily accessible attributes for useful parameters automatically evaluated during the acquisition.

Every Sensor instance implements the following methods:


* getRaw: reads a raw value from the sensor and returns it
* setNormFunc: sets a normalization function
* getNormalized: reads a raw value from the sensor and returns a normalized one
* currentSample: returns last read sample
* previousSample: returns the last but one read sample
* doEverySample: appends to a list a function to be executed every time a get function is called
* resetSampleActions: resets Actions list
* addCheck: appends to a list a couple of a condition to be checked every time a get function is called the action to be executed if the condition is verified
* resetChek: resets Checks list
* startSampling: sets a sampling interval
* stopSampling: clears the sampling interval
* wait: sleeps
* setObservationWindow: sets the length of the window used to evaluate a set of useful parameters
* setSamplingTime: sets the private attribute _samplingTime (use carefully)

Every Sensor instance provides the following parameters evaluated in a window of n acquisitions (both in sampling mode and simple get calls):


* currentAverage: moving average for last n samples
* currentDerivative: last sample minus penultimate sample, all divided by sampling time in seconds (only sampling mode)
* currentTrend: last sample minus first sample of the window, all divided by sampling time in seconds (only sampling mode)
* minSample: smallest sample of the window
* maxSample: greatest sample of the window

And the following attributes to control the process of evaluation of the parameters:


* skipEval: if True skips the whole process of evaluation
* storeAverage: if False skips average evaluation
* storeTrend: if False skips trend evaluation
* storeMinMax: if False skips min and max evaluation

## The Sensor class

##### class Sensor

```#!py3 class Sensor()```

This is the base class for generic sensors connected to pins.

###### Sensor._resetSamplingParams

```#!py3 _resetSamplingParams()```

Resets sampling parameters.

###### Sensor.setObservationWindow

```#!py3 setObservationWindow(n)```

Sets the length of the window (n) used to evaluate a set of useful parameters. Needed to evaluate those parameters during manual acquisition (calling getRaw/getNormalized functions), in sampling mode (entered by startSampling call) the length is given as a parameter of startSampling method.

!!! note
	**self._samplingTime** can be found set in:


* sampling mode: setObservationWindow should not have been called
* get mode: self._samplingTime has been manually set because samplingTime dependent parameters (like trend and derivatived) are necessary in a non-sampling mode (should be very rare)

###### Sensor.setSamplingTime

```#!py3 setSamplingTime(time)```

Manually sets _samplingTime private attribute.

!!! warning
	**Use carefully** setObservationWindow method.

This attribute is automatically set when startSampling method is called.

###### Sensor.currentSample

```#!py3 currentSample()```

Returns last read sample: stored as the last element of the buffer list.

The buffer is a list of _observationWindowN elements if the window evaluation process is not skipped, as a private attribute otherwise.

###### Sensor.previousSample

```#!py3 previousSample()```

Returns last but one read sample: stored in the buffer list (see currentSample).

!!! note
	Not available if evaluation process is skipped.

###### Sensor.getRaw

```#!py3 getRaw()```

Main acquisition method for raw data.

###### Sensor.getNormalized

```#!py3 getNormalized()```

Main acquisition method for normalized data.

###### Sensor.doEverySample

```#!py3 doEverySample(to_do)```

Appends a function to the list of those to be executed when _getValue is called.

!!! note
	*_getValue* is called both in sampling and manual acquisition mode.

Example:

```py
def out(obj):
    print(obj.currentSample())

mySensor.doEverySample(out)

### 'out' is executed in both cases:
mySensor.startSampling(...)
mySensor.getRaw()
```

Returns self to allow a compact code:

```py
mySensor.doEverySample(out).addCheck(...).startSampling(...)
```

###### Sensor.resetSampleActions

```#!py3 resetSampleActions()```

Resets _everySampleActions list.

###### Sensor.addCheck

```#!py3 addCheck(condition, to_do)```

Appends a condition to those to be checked every time _getValue is called and a function to the list of those to be executed when their conditions are verified.

‘condition’ must be a function that takes the current sensor object as a parameter and returns a boolean value:

```py
def averageGreaterThanThreshold(obj):
    if type(obj.currentAverage) != PNONE:
        if obj.currentAverage > 50:
            return True
        else:
            return False
    else:
        return False
```

‘to_do’ must be a function that takes the current sensor object as a parameter and performs some actions:

```py
def succeed(obj):
    print("Average is greater than threshold!")
    print(obj.currentAverage)
```

Returns self to allow a compact code (see doEverySample).

###### Sensor.resetCheck

```#!py3 resetCheck()```

Resets _checkFunctions and _checkConditions lists.

###### Sensor.setNormFunc

```#!py3 setNormFunc(fn)```

Sets a normalization function. A normalization function takes the last raw acquired value and the current sensor object as parameters.

Example:

```py
def normalizeData(val,obj):
    return obj.scale*(val/100)
```

It is recommended to use only *static* parameters stored in current object like scale factors... note:: In the object passed, obj.currentSample() returns the last but one read value because the buffer list is updated only after the normalization.

Returns self to allow a compact code (see doEverySample).

###### Sensor.startSampling

```#!py3 startSampling(time, observation_window, get_type, time_unit)```

Starts reading samples every _samplingTime. Length of _observationWindowN to evaluate window parameters, type of acquisition and time_unit characterize the acquisition itself.
If no observation_window is passed the evaluation of window parameters is skipped.

Returns self to allow a compact code (see doEverySample).

###### Sensor.stopSampling

```#!py3 stopSampling()```

Depending on mode:


* sampling mode: clears timer interval and stops sampling
* non sampling mode: resets sampling parameters

Returns self to allow a compact code (see doEverySample).

###### Sensor.wait

```#!py3 wait(time)```

Sleeps for *time* milliseconds and returns self to allow a compact code:

```py
mySensor.doEverySample(out).startSampling(…).wait(5000).stopSampling()
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTkyODE5NzQyOCwtMTc5Mjg0MTQyM119
-->
