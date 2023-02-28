## Interrupt Handler Responsibilities
The interrupt handler has a set of responsibilities to perform. Some are required by the framework, and some are required by the device. All interrupt handlers are required to do the following:

- **Determine if the device is interrupting and possibly reject the interrupt.** <br>
The interrupt handler must first examine the device and determine if it has issued the interrupt. If it has not, the handler must return DDI_INTR_UNCLAIMED. This step allows the implementation of device polling: it tells the system whether this device, among a number of devices at the given interrupt priority level, has issued the interrupt.

- **Inform the device that it is being serviced.**<br>
This is a device-specific operation, but it is required for the majority of devices. For example, SBus devices are required to interrupt until the driver tells them to stop. This guarantees that all SBus devices interrupting at the same priority level will be serviced.

- **Perform any I/O request-related processing.**<br>
Devices interrupt for different reasons, such as transfer done or transfer error. This step may involve using data access functions to read the device's data buffer, examine the device's error register, and set the status field in a data structure accordingly. Interrupt dispatching and processing are relatively time consuming.

- **Do any additional processing that could prevent another interrupt.**<br>
For example, read the next item of data from the device.<br>
Return ```DDI_INTR_CLAIMED```.
