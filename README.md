A Google script for excel which takes in data of updates for 1:1 sign ups and extracts tutor and student emails to Bcc via gmail to confirm a 1 on 1 session after an edit. 

<b> For practical purposes: </b> 
<ul>
  
<li> Best case scenario: <br>
   The code takes in the student name, subject name and start time of session. When a tutor adds their name (and no timing notes are provided by the student nor the tutor providing any notes), the Ops Tutor and       Student data sheets are accessed, searching for the tutor name by their tutor code (taken from the sign-up sheet by mashing first three letters of first and last name together) and the student name and last       name are searched directly. The email reference cells and the time are stored with invisible text until the emails are then found and both are bcc'd in an auto-filled email with the tutor and student's first      name, the subject and the start (and end time) of the session. When an email is successfully sent, the confirmed email cell will change to "Y" and go green and the invisible text is cleared. </br> </li>

<p>
  <li> <b> Errors </b>: 
    <br> 
    When an error occurs (see below for error types), the confirmed email cell will display "Not Confirmed" and go orange. When this occurs, the type of error will be displayed in the ops notes cell next to           it for you to identify what you need to do. There are three cells under the Ops to Fix display: Timing fixes, Tutor email and Student email. The information that is in the request that is valid will display       green in these cells. For example, if a student's email is found but they have timing requirements and a tutor's email wasn't found, the student email cell will be green and the timing fixes and tutor email       will be blank. Follow the following procedures for each error type. The stored reference cells' font from the search will go green if the confirmed email cell switches to Not Confirmed to still remain             invisible.
    </br>
    <li> 
      <ul>
        <li> 
        Timing requirements error: <br>
        The timing requirements error occurs when a the timing notes cell of the request is not empty. Be this because they're requesting a 2 hour session, a half hour session, or some other request. In this              scenario, the fix is to first check if the timing request is ok (for example if the tutor has signed up for a 2 hour session and it is in a time slot where 1:1s are running), then if it is ok, input the           time into the timing fixes cell in the format provided. This should then disappear and the cell should go green. </li> </br>
        <li>
        Tutor/Student name not found error: <br>
        The tutor name not found error occurs when the name the tutor/student uses to fulfill/put in a 1:1 request doesn't correspond to a name in the Ops Tutor/Student Data, or their first name and last name             don't match the Ops Tutor/Student Data, or their preferred name and last name don't match the Ops data. To fix this error, search the name manually in the Ops Data (via CTRL + F) and find their name. Then         copy and paste the email into the corresponding cell in the Ops fixes. This email will IMMEDIATELY disappear from the 1:1 sign-ups sheet due to conditional formatting of the sheet, having text colour set          to white if the cell is not empty, and the cell will go green. Neither name not found error means both emails need to be inputted, but the process is the same. Note that this email is not stored in the            sheet's version history since the email is immediately removed (i.e. not enough time has passed/not enough user actions have been performed for the sheet to store a new version history, so these emails            are still data-safe). </li></br>
        <li>
        Tutor notes not empty error: <br>
        The tutor has put in notes for the request. This may be that they can only do half an hour, or they can only do the first hour of a 2 hour request. In this case, alter the timing fixes in the Ops to Fix           section, which will override the current requested time to the time the tutor is available instead and change the confirmed cell to "Y" then send the email with the new time. In the case where the tutor           notes is content related or otherwise doesn't affect the Ops confirmation email (for example tutor notes says something like "Yes we can cover XYZ"), typing anything in the "Send Anyway?" cell will check          the Ops to Fix cells, and if they're green, will send the email regardless of the tutor notes, changing the confirmation email cell to "Y". If one of these cells isn't green, the confirmation email cell           will change to "Send Anyway Failed" and the Ops notes will indicate which of the three requirements failed. </br></li>
        <li>
        No time selected error: <br>
        The student has not provided a time for the request. In this case, the student needs to be emailed directly to give a time. If the time has been provided after the student has been emailed, change the             timing fix to the designated time and the confirmation email will change to "Y" and the email will send if the other two conditions are met.  </br></li>
      </ul>
    </li>
  </ul>
</p>

<p> 
<br> <b> For back-end issues:</b></br>
<br>
DISCLAIMER: You may want to consult with an Applied Computing tutor or anyone familiar with coding (in particular JavaScript or Apps Script) to troubleshoot these issues. It can be done without this knowledge, however it may be easier.</br>

<br>
The data for where information (i.e. student and tutor names, etc.) from the 1:1 sheet are taken from is based on a column. For example, student's names are extracted from column A in the 1:1 sheet, so if this changes (or any other columns such as where times, subjects, or notes - really any column) the code will fail unless the column is also updated. The code also searches for edits based on the column <i> index </i> since this is how google sheets stores column edits (it doesn't store column letters). This means that code that is supposed to execute when a tutor edits the tutor name column is actually acting from the corresponding  <i> column index </i>, 6. That is, A=1, B=2, etc. If the tutor name column changes, the code also needs to reflect that change. This also applies to searches from other sheets, as these are also  done by column. If the arrangements of other sheets changes, the columns in the code need to reflect this. 
</br>

<br>
The code also calls other sheets <i> by ID </i>. This is the random string in the URL, like the ID for the sheet 'https://docs.google.com/spreadsheets/d/1X06xgFj7Vdz77mX2BhHZShDbsi9qym_JExX-0_QyM/edit?gid=0#gid=0' (this is a fake sheet url) is '1X06xgFj7Vdz77mX2BhHZShDbsi9qym_JExX-0_QyM'. When the code calls those sheets, for the next program, the sheet ID will likely change, so the new sheet ID for the Ops Student/Tutor data spreadsheets needs to be changed. 
</br>

</p>
