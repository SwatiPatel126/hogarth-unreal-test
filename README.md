# hogarth-unreal-test
(It's unreal assessment test for Hogarth)

**Project Overview**

Title: SecuritySystemPrototype  
Engine: Unreal 5.4  
Language: Blueprint  
Description: This project demonstrates a basic Security System built in Unreal Engine 5.4 using the First Person Shooter template. The system includes a security camera that tracks player distance and direction and shows an alert. There's a Keypad that requires code entry to activate the camera.

**Objective**

Create an interactive security system consisting of:  
● A Security Camera that reacts to player movement with different light colors.  
● A Keypad that accepts a numeric code and toggles the camera's state upon successful entry.  

💠 **Security Camera System**  
        **Functionality:** 
        Detects the player’s distance and relative angle  
        Displays different light colors  
        🔴 Red: Player in front  
        🟡 Yellow: Player on the side  
        🟢 Green: Player behind or far away  

  **System Design**
  
  **Actor Blueprint:** BP_SecurityCamera  
  **Components:**  
   ● CameraBody/Box – Static Mesh (visual representation)  
   ● StatusLight/SpotLight – Point Light (color indicator)  
   ● ForwardDirection – Arrow (to get forward vector)  
  **Events:**  
    ● **EventBeginPlay**  
    - Deactivate camera  
    - Display keypad to enter passcode  
    - Set input mode to UI  
    ● **OnSuccessfulAccess**  
    - Set IsLoggedIn to true  
    - Activate camera  
    - Set input mode to game and UI  
    ● **EventTick**  
    - Get Player Character’s position  
    - Get camera body(box mesh) center position  
    - Calculate distance to player  
    - Get forward vector of camera body  
    - Calculate direction to player  
    - Use Dot Product + Acos to calculate angle(convert radian to degree)     
    - Apply light color logic based on angle  
    ● **Exposed Parameters**  
    - DetectionRadius (float)  
    - FrontalAngle (float)  
    - SideAngle (float)  

💠 **Keypad System**  
      **Functionality:**  
      ● Player can manually enter a numeric code  
      ● Displays current input  
      ● Validates input on pressing Enter  
      ● On enter press display appropriate message("Access Denied" in red color and "Access Granted" in green color)  
      ● If correct, activates the camera  

  **System Design**     
  
  **Widget Blueprint:** Keypad  
  **Components:**  
   ● Buttons 0-9, Clear, Enter  
   ● Passcode text block to disply entered passcode digits    
  **Events:**  
    ● **OnClicked**  
    - Button 0-9: Append text in passcode text block  
    - Button Clear: Clears passcode text block  
    - Button Enter: Validates entered passcode. If correct, displays "Access Granted" message in green, removes widget and executes OnSuccessful event of BP_SecurityCamera. If wrong, displays "Access Denied" in red.

   **Assumptions**  
      ● User has to enter passcode to enable security camera as well as game play(user movement).

  **Area of Improvements**  
      ● Allow user movement on game start. Keypad is activated/deactivated when user is inside the range of camera.
       
