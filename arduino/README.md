# RC Control

## Overview

This project involves a simple Arduino program that controls the direction of movement based on commands received through the Serial interface. The directions include moving forward, backward, left, right, and combinations of these movements.

## Hardware Requirements

- Arduino board
- Four output pins connected to control mechanisms for right, left, forward, and reverse movements

## Code Explanation

### Pin Definitions and Variables

```cpp
int right_pin = 6;
int left_pin = 7;
int forward_pin = 10;
int reverse_pin = 9;

int time = 50;
int command = 0;
```

- `right_pin`, `left_pin`, `forward_pin`, `reverse_pin`: Define the pin numbers used for the respective movements.
- `time`: Duration for which the output signal is active.
- `command`: Stores the received command.

### Setup Function

```cpp
void setup() {
  pinMode(right_pin, OUTPUT);
  pinMode(left_pin, OUTPUT);
  pinMode(forward_pin, OUTPUT);
  pinMode(reverse_pin, OUTPUT);
  Serial.begin(115200);
}
```

- Initializes the pins as outputs.
- Starts the Serial communication at a baud rate of 115200.

### Loop Function

```cpp
void loop() {
  if (Serial.available() > 0) {
    command = Serial.read();
  } else {
    reset();
  }
  send_command(command, time);
}
```

- Checks if there is any data available in the Serial buffer.
- Reads the command if available; otherwise, resets the output.
- Calls `send_command` to perform the appropriate action based on the received command.

### Movement Functions

- `right(int time)`, `left(int time)`, `forward(int time)`, `reverse(int time)`: Activates the respective pin for the specified duration.

```cpp
void right(int time) {
  digitalWrite(right_pin, LOW);
  delay(time);
}

void left(int time) {
  digitalWrite(left_pin, LOW);
  delay(time);
}

void forward(int time) {
  digitalWrite(forward_pin, LOW);
  delay(time);
}

void reverse(int time) {
  digitalWrite(reverse_pin, LOW);
  delay(time);
}
```

- `forward_right(int time)`, `reverse_right(int time)`, `forward_left(int time)`, `reverse_left(int time)`: Activates a combination of pins for complex movements.

```cpp
void forward_right(int time) {
  digitalWrite(forward_pin, LOW);
  digitalWrite(right_pin, LOW);
  delay(time);
}

void reverse_right(int time) {
  digitalWrite(reverse_pin, LOW);
  digitalWrite(right_pin, LOW);
  delay(time);
}

void forward_left(int time) {
  digitalWrite(forward_pin, LOW);
  digitalWrite(left_pin, LOW);
  delay(time);
}

void reverse_left(int time) {
  digitalWrite(reverse_pin, LOW);
  digitalWrite(left_pin, LOW);
  delay(time);
}
```

### Reset Function

```cpp
void reset() {
  digitalWrite(right_pin, HIGH);
  digitalWrite(left_pin, HIGH);
  digitalWrite(forward_pin, HIGH);
  digitalWrite(reverse_pin, HIGH);
}
```

- Resets all pins to HIGH, stopping all movements.

### Command Processing Function

```cpp
void send_command(int command, int time) {
  switch (command) {
    case 0: reset(); break;
    case 1: forward(time); break;
    case 2: reverse(time); break;
    case 3: right(time); break;
    case 4: left(time); break;
    case 6: forward_right(time); break;
    case 7: forward_left(time); break;
    case 8: reverse_right(time); break;
    case 9: reverse_left(time); break;
    default: Serial.print("Invalid Command\n");
  }
}
```

- Processes the received command and calls the appropriate movement or reset function based on the command value.

## Usage

1. Upload the code to the Arduino board.
2. Connect the hardware components to the appropriate pins.
3. Open the Serial Monitor and send commands to control the movements.

Commands:
- `0`: Reset
- `1`: Move forward
- `2`: Move backward
- `3`: Move right
- `4`: Move left
- `6`: Move forward-right
- `7`: Move forward-left
- `8`: Move backward-right
- `9`: Move backward-left

Make sure the Serial Monitor baud rate is set to 115200.
