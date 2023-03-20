Click on the **View tool** in the Scene view (the hand icon) and drag the view until you are positioned behind the ball.

Go to the Hierarchy window. Right-click on the 'Main Camera' and select **Align With View**. 

Go to the Inspector window for the 'Main Camera' and click on the **Add Component** button. Create a new script called `CameraController`.

Open the `CameraController` script and enter the following code:

--- code ---
---
language: cs
filename: CameraController.cs
line_numbers: true
line_number_start: 1
line_highlights: 
---

using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class CameraController : MonoBehaviour
{
  public float sensitivity = 5f;
  public GameObject ball;
  private Vector3 prevBallPos;

  void Start()
   {
       // Calculate where the camera is in relation to the player (ball)
       transform.LookAt(ball.transform);
       prevBallPos = ball.transform.position;
   }

void LateUpdate()
   {
       float mouse = Input.GetAxis("Mouse Y");
       transform.Rotate(new Vector3(mouse * sensitivity * -1, 0, 0));
       float look = Input.GetAxis("Mouse X") * sensitivity;
       transform.RotateAround(ball.transform.position, Vector3.up, look);
       // Moves the camera by the same amount the ball has moved
       transform.Translate(ball.transform.position - prevBallPos, Space.World);
       prevBallPos = ball.transform.position;
   }
}

--- /code ---

**Save** and return to Unity.

With the 'Main Camera' selected, drag the `Ball` GameObject to the `Ball` variable in the Inspector window inside your `CameraController` script.
