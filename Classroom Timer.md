---
tags:
  - step-by-step-guide
date: 2023-09-02 14:26
File Modified: 2023-09-19 10:22
File Folder: ClassroomTimer
Type: Code
aliases:
  - U14
  - Timer
  - C#
Tag:
---

---
#step-by-step-guide
# Instructions

Steps to  follow to create a classroom timer application with a graphical user interface (GUI) in C# using Windows Forms and the `System.Windows.Forms.Timer` control:

**Creating a Classroom Timer Application**

In this project, you will create a classroom timer with a user-friendly GUI. The timer will count down from a specified duration and trigger an alarm when the time is up.

**Step 1: Create a New Windows Forms Application Project**

1. Open Visual Studio.
2. Go to "File" > "New" > "Project..."
3. Select "Windows Forms App (.NET Core)" or a similar project template.
4. Give your project a name (e.g., "ClassroomTimer") and click "Create."

**Step 2: Design the Timer Interface**

1. In the Solution Explorer, find and double-click on "Form1.cs" (or similar) to open the Windows Form Designer.

**Step 3: Add GUI Elements**

1. From the "Toolbox" on the left, drag and drop the following controls onto the form:
   - TextBox: For entering the timer duration (name it "durationTextBox").
   - Button: For starting and stopping the timer (name it "startButton").
   - Another TextBox: For displaying the remaining time (name it "timerTextBox").
2. Adjust the size and position of these controls as needed.

**Step 4: Set Control Properties**

1. For the "durationTextBox":
   - Set its `Name` property to "durationTextBox."
2. For the "startButton":
   - Set its `Name` property to "startButton."
   - Set its `Text` property to "Start."
3. For the "timerTextBox":
   - Set its `Name` property to "timerTextBox."
   - Set its `Enabled` property to `False` to prevent user input.
   - Set its `Text` property to an initial value (e.g., "00:00").

    ![Imgur](https://i.imgur.com/m7SZ7k2.png)

**Step 5: Customize the Form Properties**

1. Click on the form itself to select it.
2. Set its `Text` property to something like "Classroom Timer."

**Step 6: Write Code for the Timer**

1. In the code-behind file (e.g., "Form1.cs"), replace the existing code with the code provided below.
2. This code initializes the timer, starts and stops the countdown, and handles the alarm event.
3. Ensure that the code is correctly placed in the appropriate sections of your form's class.

```csharp
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;

namespace SimpleCalculator
{
    public partial class Form1 : Form
    {
        private int remainingSeconds; // Variable to store remaining seconds
        private Timer timer; // Timer for the countdown

        public Form1()
        {
            InitializeComponent();
        }

        private void Form1_Load(object sender, EventArgs e)
        {
            // Initialize the form and controls
            durationTextBox.Text = "00:00";
            timer = new Timer();
            timer.Interval = 1000; // 1 second interval
            timer.Tick += new EventHandler(TimerCallback);
            timer.Enabled = false; // Timer is initially disabled
        }

        private void timerTextBox_TextChanged(object sender, EventArgs e)
        {
            // Display the entered time in the durationTextBox
            durationTextBox.Text = timerTextBox.Text;
        }

        private void startButton_Click(object sender, EventArgs e)
        {
            // Start or pause the timer when the button is clicked
            if (!timer.Enabled)
            {
                if (int.TryParse(timerTextBox.Text, out int minutes))
                {
                    if (minutes >= 1 && minutes <= 30)
                    {
                        // Calculate total seconds from minutes
                        remainingSeconds = minutes * 60;

                        // Enable the timer and disable user input for timerTextBox
                        timer.Enabled = true;
                        timerTextBox.Enabled = false;
                    }
                    else
                    {
                        MessageBox.Show("Please enter a valid number between 1 and 30 for the duration.");
                    }
                }
                else
                {
                    MessageBox.Show("Please enter a valid number for the duration.");
                }
            }
            else
            {
                // Pause the timer
                timer.Enabled = false;
                timerTextBox.Enabled = true; // Enable user input
            }
        }

        private void TimerCallback(object sender, EventArgs e)
        {
            // Timer callback event handler code goes here
            if (remainingSeconds > 0)
            {
                remainingSeconds--;

                // Update timerTextBox with remaining time
                int minutes = remainingSeconds / 60;
                int seconds = remainingSeconds % 60;
                timerTextBox.Text = $"{minutes:D2}:{seconds:D2}";
            }
            else
            {
                // Timer has reached 0, display "TIME UP!" and stop the timer
                timerTextBox.Text = "TIME UP!";
                timer.Enabled = false;
                timerTextBox.Enabled = true; // Enable user input
            }
        }

        private void durationTextBox_TextChanged(object sender, EventArgs e)
        {
            // durationTextBox.TextChanged event handler code goes here
        }
    }
}
```

**Step 7: Test Your Timer**

1. Build and run your application to test the timer functionality.
2. Verify that it counts down and triggers the alarm when it reaches 0.

**Step 8: Enhance the Alarm Event (Optional)**

1. If desired, customize the alarm event further by adding sound or additional actions.

**Step 9: Build and Deploy**

1. Once you're satisfied with your classroom timer application, build and deploy it as needed.

These step-by-step instructions should help you create a basic classroom timer GUI in Visual Studio using C# and Windows Forms. You can further customise the design and add additional features as desired.

![Imgur](https://i.imgur.com/XllBXAO.png)
