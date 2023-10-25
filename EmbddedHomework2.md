 # Embdded System Design Homework 2 
 ## Harshit Tak (EE23MT007)

  Develop the architecture for an embedded system to control
		a windshield wiper system. A windshield wiper motor assembly
		is available and has one digital in (RUN) and one digital out
		(HOME). As long as the RUN line is held high, the motor runs
		and the wiper operates continuously, i.e wipes back and forth.
		Whenever the wiper is in the lowest position, the HOME line
		goes low, when the wiper is elsewhere it is high.
		
		Your task is to design an embedded controller that is capable
		of operating this wiper in three modes - 
		a) continuously wiping (for heavy rain)
		b) intermittent (wipe once, wait, wipe once, wait, etc)
		c) wipe exactly once and then stop
		
		Your design should also include how you will take input from
		the user (the driver of the vehicle) in an intuitive way- i.e.
		the user should not need to know the internal workings of the
		system. You should also ensure that the wiper is never stopped
		in the "up" state- i.e. your controller should always make sure
		to run the motor till the wiper comes down and then stop.

  There is one input Run which is high then the wiper start working and one oputput Home which is telling the position of wiper which is to coniferm that the wiper should always switch off in dowm position.

  Below is the flowchart diagram for the repesentation of the problem

  ## Flochart
  
  ![FlowChart](https://github.com/HarshitTak/Test/blob/main/WhatsApp%20Image%202023-10-25%20at%2010.54.43%20PM.jpeg)


  ## Psudocode
  ``` C
   int main() {
    GPIO_INIT();  // Initializes GPIO pins
    int state = 0;  // Initialize the state variable
    int run = 0;
    int home = 0;
    int current_state = 0;

    while (1) {
        state = GPIO_READ();  // Read the state from GPIO pins

        if (state == 0) {
            run = 1;
            while (home != 0) {
                // Keep running the motor until the wiper is in the lowest position
                run = 1;
            }
            run = 0;
        } else if (state == 1) {
            current_state = state;
            while (current_state == state) {
                // Keep running the motor in continuous mode
                run = 1;
            }
        } else if (state == 2) {
            current_state = state;
            while (current_state == state) {
                // Keep running the motor in intermittent mode
                run = 1;
                while (home != 0) {
                    // Keep running the motor until the wiper is in the lowest position
                    run = 1;
                }
                run = 0;
                delay();  // You should define the delay function
            }
        } else if (state == 3) {
            run = 1;
            state = 0;  // Change the state back to continuous mode
        }

        state = GPIO_READ();
    }
}

```

