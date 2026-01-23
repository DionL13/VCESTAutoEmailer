A Google script for excel which takes in data of updates for 1:1 sign ups and extracts tutor and student emails to Bcc via gmail to confirm a 1 on 1 session after an edit. 

<b> For practical purposes: </b> 
<ul>
  
<li> Best case scenario: <br>
   The code takes in the student name, subject name and start time of session. When a tutor adds their name (and no timing notes are provided by the student nor the tutor providing any notes), the Ops Tutor and       Student data sheets are accessed, searching for the tutor name by their tutor code (taken from the sign-up sheet by mashing first three letters of first and last name together) and the student name and last       name are searched directly. The emails are then found and both are bcc'd in an auto-filled email with the tutor and student's first name, the subject and the start (and end time) of the session. When an           email is successfully sent, the confirmed email cell will change to "Y" and go green.</br> </li>

<p>
  <li> <b> Errors </b>: 
    <br> 
    When an error occurs (see below for error types), the confirmed email cell will display "Not Confirmed" and go orange. When this occurs, the type of error will be displayed in the ops notes cell next to           it for you to identify what you need to do. There are three cells under the Ops to Fix display: Timing fixes, Tutor email and Student email. The information that is in the request that is valid will display       green in these cells. For example, if a student's email is found but they have timing requirements and a tutor's email wasn't found, the student email cell will be green and the timing fixes and tutor email       will be blank. Follow the following procedures for each error type. </br>
    <li> 
      <ul>
        <li> Timing Requirements Error: <br>
        The timing requirements error occurs when a the timing notes cell of the request is not empty. Be this because they're requesting a 2 hour session, a half hour session, or some other request. In this                 scenario, the fix is to first check if the timing request is ok (for example if the tutor has signed up for a 2 hour session and it is in a time slot where 1:1s are running), then if it is ok, input the time       into the timing fixes cell in the format provided. This should then disappear and the cell should go green. </li> </br>
      </ul>
      
    </li>
  </ul>
</p>
