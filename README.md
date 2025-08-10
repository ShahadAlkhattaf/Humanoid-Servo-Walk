# Walking Motion Using Servo Motors

## Objective
Develop and simulate an algorithm to control **4 servo motors** for simulating a walking motion in a humanoid robot.  
This simulation is implemented using **Tinkercad Circuits** and **Arduino code**.

---

## Components Used
- **Microcontroller**: Arduino Uno  
- **Servo Motors**: 4  
  - Servo 1: Right Hip  
  - Servo 2: Right Knee  
  - Servo 3: Left Hip  
  - Servo 4: Left Knee  
- **Tinkercad Circuits**: For simulation  
- **Jumper Wires** and **Breadboard**

---

## 💻 Arduino Code
```cpp
#include <Servo.h>

// Create servo objects for each motor
Servo myservo1, myservo2, myservo3, myservo4;

void setup() {
  // Attach servos to pins
  myservo1.attach(2);
  myservo2.attach(3);
  myservo3.attach(4);
  myservo4.attach(5);

  // Perform one sweep: 0 -> 180
  for (int pos = 0; pos <= 180; pos++) {
    moveAllServos(pos);
    delay(15);  // Wait for servo to reach the position
  }

  // Then sweep back: 180 -> 0
  for (int pos = 180; pos >= 0; pos--) {
    moveAllServos(pos);
    delay(15);
  }

  // Hold all servos at 90 degrees
  moveAllServos(90);
}

void loop() {
  // No repeated actions required
}

// Helper function to move all servos to the same position
void moveAllServos(int angle) {
  myservo1.write(angle);
  myservo2.write(angle);
  myservo3.write(angle);
  myservo4.write(angle);
}
```

---

## Circuit Preview

<img src="screenshot" width = 400>

---

## Algorithm: Humanoid Robot Walking Motion

### 1. Initialization
- **Attach Servos:** Connect hip and knee servos to microcontroller pins.  
- **Set Neutral Positions:** Initialize both servos at ~90° to simulate standing.

### 2. Define Parameters
- **Step Length**  
- **Foot Lift Height**  
- **Speed** *(Delay between moves)*

### 3. Walking Loop (Per Leg)

#### ➤ Lift the Leg:
- **Hip Servo:** Increase angle *(e.g., 90° → 120°)*  
- **Knee Servo:** Decrease angle to lift foot *(e.g., 90° → 60°)*  
- **Delay:** Small pause to ensure smooth motion

#### ➤ Swing Leg Forward:
- **Hip Servo:** Return to 90° or swing forward  
- **Knee Servo:** Straighten *(e.g., 60° → 90°)*  

#### ➤ Lower the Leg:
- **Knee Servo:** Lower the foot *(e.g., 90° → 120°)*  
- **Hip Servo:** Stabilize *(keep at 90°)*  

#### ➤ Shift Weight:
- Adjust the opposite hip servo to shift body weight to the front leg

### 4. Repeat for Opposite Leg
- Mirror the above sequence for the other leg.

### 5. Continuous Loop
- Repeat the walking cycle with continuous angle/speed adjustments for both hips and knees to maintain balance and motion.
