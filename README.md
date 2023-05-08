Download Link: https://assignmentchef.com/product/solved-sdev300-lab8
<br>
<strong>WAMP ZAP Analysis and Mitigation </strong>

<strong>Overview </strong>

For this final lab you will use the tools and techniques used throughout the course to analyze, mitigate and document the results of a WAMP applications. The application to analyze uses a prototype UMUC tutoring application that allows a tutor to login, upload their resume, sign a guest book and view and delete tutor assignments. You will need to install the application on the SDEV AMI, run the analysis using ZAP, manual interceptions and code review, fix all vulnerabilities and document the results.

<strong>Learning Outcomes: </strong>

At the completion of the lab you should be able to:

<ol>

 <li>Set-up and run the UMUC tutor application on your VM</li>

 <li>Conduct automated and manual analysis on a LAMP application</li>

 <li>Identify, prioritize and repair software vulnerabilities found in the application 4. Document the process, findings and specifics on how you resolved the issues.</li>

</ol>

<strong> </strong>

<strong>Lab Submission Requirements: </strong>

After completing this lab, you will submit a word (or PDF) document that meets all of the requirements in the description at the end of this document. In addition, your associated files should be submitted. Those associated files will be the original files as well as a complete set of files with fixes implemented. You should submit multiple files in a winzip file.

<strong> </strong>

<strong>Virtual Machine Account Information </strong>

Your Virtual Machine has been preconfigured with all of the software you will need for this class. You have connected to this machine in the previous labs. Reconnect again using the Remote Desktop connection, your Administrator username and password.

<strong> </strong>

<strong>Tutor Application user accounts: </strong>

<table width="623">

 <tbody>

  <tr>

   <td width="312"><strong>Username </strong></td>

   <td width="312"><strong>Password </strong></td>

  </tr>

  <tr>

   <td width="312">tutor1</td>

   <td width="312">t123</td>

  </tr>

  <tr>

   <td width="312">tutor2</td>

   <td width="312">t234</td>

  </tr>

  <tr>

   <td width="312">tutor3</td>

   <td width="312">t345</td>

  </tr>

 </tbody>

</table>

<strong> </strong>




<strong>Part 1 – Set-up and Run the UMUC tutor application on your VM </strong>

In this exercise you will create and populate the database tables for the WAMP application and install the PHP and associated files on your VM. The application is fully functional (but definitely not safe or secure). You need to perform a few steps to make sure it is working properly on your VM.

<ol>

 <li>Attached to this Project is zip folder. Download the BadTutor.zip file and upload to your SDEV AMI VM. The BadTutor.zip file contains the Web Application as well as SQL folder with SQL scripts to create the databases and tables needed for this application.</li>

</ol>










<ol start="2">

 <li>Once uploaded to the SDEV AMI, unzip the file and place the BadTutor folder in the htdocs folder as shown in figure 1.</li>

</ol>

<img decoding="async" data-recalc-dims="1" data-src="https://i0.wp.com/www.ankitcodinghub.com/wp-content/uploads/2020/01/583.png?w=980&amp;ssl=1" class="lazyload" src="data:image/gif;base64,R0lGODlhAQABAAAAACH5BAEKAAEALAAAAAABAAEAAAICTAEAOw==">

 <noscript>

  <img decoding="async" src="https://i0.wp.com/www.ankitcodinghub.com/wp-content/uploads/2020/01/583.png?w=980&amp;ssl=1" data-recalc-dims="1">

 </noscript>

<em>Figure 1 Move BadTutor to the htdocs folder </em>




Next, we will open up the SQL folder and run the database scripts. This is a critical step needed so the Web application can properly communicate with the database.

<ol>

 <li>Open your command prompt and change to the BitnamiWampStack-7.1.16-0mysqlbin directory and enter the following command:</li>

</ol>

mysql –u root –p

When prompted enter the following mysql root password:

sdev300vm99










<ol start="2">

 <li>Next, we will run the database scripts in their entirety using the “source” option for MySQL. This will run each of the two SQL scripts without any real human intervention.</li>

</ol>

To run the scripts you will need to copy and paste or type the following commands at the MySQL prompt:

source C:Bitnamiwampstack-7.1.16-0apache2htdocsBadTutorSQLDBSetup.sql source C:Bitnamiwampstack-7.1.16-0apache2htdocsBadTutorSQLSQLCode.sql

Note, the source command is used to run any SQL file. You just need to fully define the location

(including the path).  Figure 2 show the results of running the first Scripts which sets-up the database.

<img decoding="async" data-recalc-dims="1" data-src="https://i0.wp.com/www.ankitcodinghub.com/wp-content/uploads/2020/01/367-1.png?w=980&amp;ssl=1" class="lazyload" src="data:image/gif;base64,R0lGODlhAQABAAAAACH5BAEKAAEALAAAAAABAAEAAAICTAEAOw==">

 <noscript>

  <img decoding="async" src="https://i0.wp.com/www.ankitcodinghub.com/wp-content/uploads/2020/01/367-1.png?w=980&amp;ssl=1" data-recalc-dims="1">

 </noscript>

<em>Figure 2 Running the DBSetup.sql script </em>

Use of the show database; command before and after the set-up reveals the addition of the new tutors database. Be sure to carefully, review and understand each statement in the SQL script files.

Figure 3 shows the results of running the second SQL script. In this script, the tables are created and an initial set of data is populated for testing purposes.

<img decoding="async" data-recalc-dims="1" data-src="https://i0.wp.com/www.ankitcodinghub.com/wp-content/uploads/2020/01/114.png?w=980&amp;ssl=1" class="lazyload" src="data:image/gif;base64,R0lGODlhAQABAAAAACH5BAEKAAEALAAAAAABAAEAAAICTAEAOw==">

 <noscript>

  <img decoding="async" src="https://i0.wp.com/www.ankitcodinghub.com/wp-content/uploads/2020/01/114.png?w=980&amp;ssl=1" data-recalc-dims="1">

 </noscript>

<em>Figure 3 Running the SQLCode.sql file </em>

You should run some queries to make sure your database scripts functioned properly. If they didn’t, you can actually, drop the database and start again with the drop database tutors; command.

Some simple queries to test your tables are shown below:

x Use tutors; x Select * from TutorDetails; x Select * from  StudentSchedules; x Select * from TutorSchedules; x Select * from GroupSchedules; x Select * from CourseGroups; x Select * from TutorGroups; x Select * from Students; x Select * from Semesters; x Select * from Courses; x Select * from Tutors;

x Select * from GuestBook;




Compare the results to the SQL files before proceeding to the next steps. If your database data is not correct, you won’t be able to test your application.







Next, we will test to make sure the Web application is working.

<ol start="5">

 <li>Reset the httponly security option in your httpd.conf file</li>

</ol>

If you properly corrected the vulnerabilities and environment settings in week 5, you most likely added something similar to this statement in your httpd.conf file

Header edit Set-Cookie ^(.*)$ $1;HttpOnly;Secure

For this BadTutor application to function, you will need to comment out that line with a #:

#  Header edit Set-Cookie ^(.*)$ $1;HttpOnly;Secure

Also, be sure to stop and restart the Apache server for this change to take effect.

Now, the fact that we have to comment out a security protection to get an application to work should speak loudly to you about a security issue in this application. However; these is also some functionality associated with the application that is required. So when you fix the security issues you can’t just break the application. You have to provide a better design that allows the desired functionality to be implemented securely. This is not always easy and often requires some risk assessment and trade-offs.

<ol start="6">

 <li>Open up your Browser and Launch the BadTutor app (localhost/BadTutor)</li>

</ol>

As shown in figure 4, you should be able to login using one of the 3 tutor credentials listed earlier in the document, or click on the links to upload a resume or sign the guest book. (Note: Be sure you have modified the FireFox proxy options to “No Proxy”)

<img decoding="async" data-recalc-dims="1" data-src="https://i0.wp.com/www.ankitcodinghub.com/wp-content/uploads/2020/01/787.png?w=980&amp;ssl=1" class="lazyload" src="data:image/gif;base64,R0lGODlhAQABAAAAACH5BAEKAAEALAAAAAABAAEAAAICTAEAOw==">

 <noscript>

  <img decoding="async" src="https://i0.wp.com/www.ankitcodinghub.com/wp-content/uploads/2020/01/787.png?w=980&amp;ssl=1" data-recalc-dims="1">

 </noscript>

<em>Figure 4 Testing the BadTutor Application </em>

You should sign In with each of the tutor credentials, and experiment with all of the functionality so you understand what the application is designed to do. (Hint: Do you think those passwords are secure?)







<ol start="6">

 <li>Go through each link in the application testing the functionality so you fully understand the intent and purpose of the application. Login in as different tutors as you test the application. After you complete your security analysis and fixes, the baselines functionality should still be present but much more secure.</li>

</ol>




Figures 5 – 17 shows the results of running the application for the tutor1 user and deleting a tutor session, uploading a resume and signing the guest book.

<em><img decoding="async" data-recalc-dims="1" data-src="https://i0.wp.com/www.ankitcodinghub.com/wp-content/uploads/2020/01/113.png?w=980&amp;ssl=1" class="lazyload" src="data:image/gif;base64,R0lGODlhAQABAAAAACH5BAEKAAEALAAAAAABAAEAAAICTAEAOw==">

  <noscript>

   <img decoding="async" src="https://i0.wp.com/www.ankitcodinghub.com/wp-content/uploads/2020/01/113.png?w=980&amp;ssl=1" data-recalc-dims="1">

  </noscript></em>

<em>Figure 5 Select Delete Session</em>

<img decoding="async" data-recalc-dims="1" data-src="https://i0.wp.com/www.ankitcodinghub.com/wp-content/uploads/2020/01/292.png?w=980&amp;ssl=1" class="lazyload" src="data:image/gif;base64,R0lGODlhAQABAAAAACH5BAEKAAEALAAAAAABAAEAAAICTAEAOw==">

 <noscript>

  <img decoding="async" src="https://i0.wp.com/www.ankitcodinghub.com/wp-content/uploads/2020/01/292.png?w=980&amp;ssl=1" data-recalc-dims="1">

 </noscript>




<img decoding="async" data-recalc-dims="1" data-src="https://i0.wp.com/www.ankitcodinghub.com/wp-content/uploads/2020/01/451.png?w=980&amp;ssl=1" class="lazyload" src="data:image/gif;base64,R0lGODlhAQABAAAAACH5BAEKAAEALAAAAAABAAEAAAICTAEAOw==">

 <noscript>

  <img decoding="async" src="https://i0.wp.com/www.ankitcodinghub.com/wp-content/uploads/2020/01/451.png?w=980&amp;ssl=1" data-recalc-dims="1">

 </noscript>




<img decoding="async" data-recalc-dims="1" data-src="https://i0.wp.com/www.ankitcodinghub.com/wp-content/uploads/2020/01/891.png?w=980&amp;ssl=1" class="lazyload" src="data:image/gif;base64,R0lGODlhAQABAAAAACH5BAEKAAEALAAAAAABAAEAAAICTAEAOw==">

 <noscript>

  <img decoding="async" src="https://i0.wp.com/www.ankitcodinghub.com/wp-content/uploads/2020/01/891.png?w=980&amp;ssl=1" data-recalc-dims="1">

 </noscript>

<img decoding="async" data-recalc-dims="1" data-src="https://i0.wp.com/www.ankitcodinghub.com/wp-content/uploads/2020/01/545.png?w=980&amp;ssl=1" class="lazyload" src="data:image/gif;base64,R0lGODlhAQABAAAAACH5BAEKAAEALAAAAAABAAEAAAICTAEAOw==">

 <noscript>

  <img decoding="async" src="https://i0.wp.com/www.ankitcodinghub.com/wp-content/uploads/2020/01/545.png?w=980&amp;ssl=1" data-recalc-dims="1">

 </noscript>

<em>Figure 17 Logging into MySQL – tutors database and verifying data input </em>




You should experiment with the application as needed to learn the functionality.

Note, the application is used to review and delete tutoring sessions. In this case, sessions refer to a 30 minute meeting between a student and the tutor. This is not the same as Web application or HTTP sessions. The HTTP sessions within this PHP application are the heart of the functionality as well as the vulnerabilities for this application.

<strong>Lab submission details: </strong>

As part of the submission for this Lab, you will run manual and automatic attacks on you’re the BadTutor Web application. Be sure to carefully review the code for obvious security issues and information leakage.

You can provide the findings in one well-organized document. You should work to eliminate all alerts in the application and clearly document specifically what you did to mitigate each issue.

Create screen captures demonstrating your process and results.  Each screen capture should be fully described. The document should be well-organized and include a table of contents, page numbers, figures, and table numbers. The writing style should be paragraph style with bullets used very sparingly to emphasize specific findings. In other words, this should be a professional report and demonstrate mastery of writing.

When researching your security alerts, be sure to document your references using APA style.  You should show both before and after fix vulnerability reports. Your final vulnerability report should show zero alerts and vulnerabilities; or fully describe why an alert was not eliminated.

For your deliverables, you should submit a zip file containing your word document (or PDF file) along with the before and after application files.  (including SQL and parameter files) If you made changes to your VM environment (apache2.conf, php.ini) you should provide those files also.

Include your full name, class number, professor name and section and date in the document.




<strong>Grading Rubric: </strong>

<table width="600">

 <tbody>

  <tr>

   <td width="126"><strong>Attribute </strong></td>

   <td width="474"><strong>Meets </strong></td>

  </tr>

  <tr>

   <td width="126">Analysis, Scans and Mitigation</td>

   <td width="474"><strong>60 points </strong>Provides through and detailed analysis on the application including manual code reviews and comments, manual ZAP interceptions and Automated ZAP analysis (40 points) Fully describes and eliminates all alerts and vulnerabilities or fully describes why an alert was not eliminated. (20 points)</td>

  </tr>

  <tr>

   <td width="126">Documentation and submission</td>

   <td width="474"><strong>40 points </strong>Submits a word or PDF document that includes screen captures demonstrating your process and results. Screen captures are fully described. Clearly documents specifically what you did to mitigate each issue. (20 points) </td>

  </tr>

  <tr>

   <td width="126"> </td>

   <td width="474">Document is well-organized and includes a table of contents, page numbers, figures and table numbers. The writing style should be paragraph style with bullets used very sparingly to emphasize specific findings.  Document your references using APA style.  (10 points) Includes all before and after application files in winzip format.  (SQL and parameter files, apache2.conf, php.ini) (10 points)</td>

  </tr>

 </tbody>

</table>

<strong> </strong>

<strong> </strong>

A couple of quick hints:

<ol>

 <li>Start early as this will take some time.</li>

 <li>Be sure your application is working properly before you start running the security analysis.</li>

 <li>Ask questions if you are stuck or have technical issues.</li>

 <li>Secure HTTP Sessions are key and they should be hard to guess and randomly generated.</li>

 <li>SQL injection, SQL injection … SQL Injection. Need I say more?</li>

 <li>I log in, but shouldn’t I be able to logout?</li>

 <li>Feel free to make the resultant application nicer and more user friendly.</li>

</ol>


