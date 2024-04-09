# robot-for-disasters
he robot is equipped with sensors to detect obstacles, temperature, and possibly gas leaks. It also assumes the robot has motors for locomotion
// Include necessary libraries
#include <Servo.h>

// Define pins for sensors
#define OBSTACLE_SENSOR_PIN 2
#define TEMPERATURE_SENSOR_PIN A0
#define GAS_SENSOR_PIN A1

// Define pins for motor control
#define LEFT_MOTOR_PIN1 3
#define LEFT_MOTOR_PIN2 4
#define RIGHT_MOTOR_PIN1 5
#define RIGHT_MOTOR_PIN2 6

// Define servo pins for arm movement
#define ARM_SERVO_PIN 9

// Define threshold values
#define OBSTACLE_THRESHOLD 200
#define MAX_TEMPERATURE 50 // Example threshold temperature in Celsius
#define GAS_THRESHOLD 500 // Example threshold gas level

// Create servo object
Servo armServo;

void setup() {
  // Initialize serial communication
  Serial.begin(9600);

  // Initialize pins for sensors
  pinMode(OBSTACLE_SENSOR_PIN, INPUT);
  
  // Initialize pins for motor control
  pinMode(LEFT_MOTOR_PIN1, OUTPUT);
  pinMode(LEFT_MOTOR_PIN2, OUTPUT);
  pinMode(RIGHT_MOTOR_PIN1, OUTPUT);
  pinMode(RIGHT_MOTOR_PIN2, OUTPUT);

  // Initialize servo
  armServo.attach(ARM_SERVO_PIN);
}

void loop() {
  // Read sensor data
  int obstacleDistance = analogRead(OBSTACLE_SENSOR_PIN);
  float temperature = getTemperature();
  int gasLevel = analogRead(GAS_SENSOR_PIN);

  // Check for obstacles
  if (obstacleDistance > OBSTACLE_THRESHOLD) {
    // Move forward
    moveForward();
  } else {
    // Stop
    stopMoving();

    // Perform obstacle avoidance or navigation algorithm here
  }

  // Check temperature
  if (temperature > MAX_TEMPERATURE) {
    // Perform cooling action or shutdown
    // Example: activate cooling fan
    // Example: send alert
  }

  // Check gas level
  if (gasLevel > GAS_THRESHOLD) {
    // Perform evacuation or mitigation action
    // Example: activate gas masks
    // Example: send alert
  }

  // Example: Perform other tasks such as sending telemetry data, etc.
  // sendTelemetryData(obstacleDistance, temperature, gasLevel);
}

float getTemperature() {
  // Read temperature sensor and convert to Celsius
  // Example code; replace with actual temperature sensor code
  int rawValue = analogRead(TEMPERATURE_SENSOR_PIN);
  float voltage = (rawValue / 1024.0) * 5.0;
  float temperatureC = (voltage - 0.5) * 100.0;
  return temperatureC;
}

void moveForward() {
  // Example: Control motors to move the robot forward
  // Code to control motors to move forward
}

void stopMoving() {
  // Example: Stop the robot
  // Code to stop the motors
}


