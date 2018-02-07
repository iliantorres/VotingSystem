# VotingSystem
Assembly voting system to manage student assemblies from the the University of Puerto Rico, Río Piedras
Database 
Database 2Fast4U
Class, Primary keys, keys and Attribute definitions:

User
user_id: (Primary key). The user_id is for identifying each unique user. The data type is varchar of size 10 that is randomly generated using UUID() and is unique to each user.
username:The username the user chooses for login purposes. Data type is character of size 20 and is unique to each user.
name: The first name the user chooses to identify himself. Data type is character of size 20.
last_name: The last name the user chooses to identify him or herself. Data type is character of size 20.
user_type: The type of user that is being created, either student or organizer. Data type is character of size 20. 
password: A secret word for login in/ signing up for the security of all users.Data type is varchar of size 30.
email: An email as a secondary contact for the any of the users. Data type is character of size 30and is unique to each user.
student_number: A student number that is unique to each student. Data type is varchar of size 10and is unique to each user.
Date_created: Date in which the group was created. Data type is current_timestamp of format mm/dd/yyhh:mm:ss

CREATE TABLE `User` (
  `user_id` varchar(10) NOT NULL,
  `username` varchar(20) NOT NULL,
  `name` varchar(20) NOT NULL,
  `last_name` varchar(20) NOT NULL,
  `user_type` varchar(20) NOT NULL,
  `password` varchar(30) NOT NULL,
  `email` varchar(30) NOT NULL,
  `student_number` varchar(15) NOT NULL,
  `date_created` datetime DEFAULT NULL,
   PRIMARY KEY (`user_id`),
   CONSTRAINT UC_User UNIQUE (user_id,username,email,student_number)
) ENGINE=InnoDB DEFAULT CHARSET=latin1;


INSERT INTO `User` (`user_id`, `username`, `name`, `last_name`, `user_type`,`password`,`email`,`student_number`,`date_created`) VALUES
(UUID(), 'TheDoctor', 'NoOne','Knows', 'Staff','SaraJane', 'testsubject1@gmail.com', '801-44-7821',CURRENT_TIMESTAMP()),
(UUID(), 'DoctorStrange', 'Steven','Strange', 'User','StrangeisBest','testsubject2@gmail.com', '555-12-8892',CURRENT_TIMESTAMP()),
(UUID(), 'JessiJones', 'Jessica','Jones', 'User','KillKillgrave', 'testsubject3@gmail.com','685-17-0098',CURRENT_TIMESTAMP()),
(UUID(), 'FlashMaster', 'Barry','Allen', 'User','FastestManAlive', 'testsubject4@gmail.com', '582-99-2201',CURRENT_TIMESTAMP()),
(UUID(), 'Samuroid', 'DeVoe','Christopher', 'User','BrainEnhance', 'testsubject5@gmail.com', '593-86-9175',CURRENT_TIMESTAMP()),
(UUID(), 'BlackList', 'Redington','Raimond', 'Staff','Dembe', 'testsubject6@gmail.com', '846-92-3027',CURRENT_TIMESTAMP()),
(UUID(), 'IronFist', 'Danny','Rand', 'User','Kuun-Lun', 'testsubject7@gmail.com', '801-93-9927',CURRENT_TIMESTAMP()),
(UUID(), 'DareDevil', 'Matt','Murdock', 'User', 'Blind', 'testsubject8@gmail.com', '893-13-3047',CURRENT_TIMESTAMP()),
(UUID(), 'Vibe', 'Sisco','Ramon', 'User', 'Technokid', 'testsubject9@gmail.com', '893-13-3047',CURRENT_TIMESTAMP());




Queries Examples: 

See all the data for a specific user:

SELECT * FROM User  WHERE username="TheDoctor"

Queries General: 

UsernameInput="TheDoctor"

SELECT * FROM User  WHERE username=UsernameInput 


Insert General:
UIusername='TheDoctor'
UIName       ='NoOne'
UIlast_name='Knows'
UIType        ='Staff'
UIPassword ='SaraJane'
UIEmail	      ='testsubject1@gmail.com'
UISNumber ='801-44-7821'

INSERT INTO `User` (`user_id`, `username`, `name`, `last_name`, `user_type`,`password`,`email`,`student_number`,`date_created`) VALUES
(UUID(),UIusername, UIName  , UIlast_name, UIType  , UIPassword, UIEmail, UISNumber,CURRENT_TIMESTAMP());
 

































User_Confirmation:
user_confirmationID: (Primary key). The user_ confirmationID is for identifying each unique user confirmation. The data type is varchar of size 10 that is randomly generated using UUID() and is unique to each user.
username:The username the user chooses for login purposes. Data type is character of size 20 and is unique to each user.
email: An email as a secondary contact for the any of the users. Data type is character of size 30 and is unique to each user.
Email_key: A key randomly generated to verify the users email. Data type  is varchar of size 20 



CREATE TABLE `User_Confirmation` (
  `user_confirmationID` varchar(10) NOT NULL,
  `username` varchar(20) NOT NULL,
  `email` varchar(30) NOT NULL,
  `Email_key`    varchar(20) NOT NULL,
   PRIMARY KEY (`user_confirmationID`),
   CONSTRAINT UC_User UNIQUE (`Email_key`)
) ENGINE=InnoDB DEFAULT CHARSET=latin1;


INSERT INTO `User_Confirmation`(`user_confirmationID`, `username`, `email`, `Email_key`) 
SELECT UUID(), username, 'testsubject1@gmail.com', UUID()
FROM User
WHERE username='TheDoctor' 

INSERT INTO `User_Confirmation`(`user_confirmationID`, `username`, `email`, `Email_key`) 
SELECT UUID(), username, 'testsubject6@gmail.com', UUID()
FROM User
WHERE username= 'BlackList'

How to delete from table:

DELETE FROM User_Confirmation WHERE username='JessiJones'


Queries:
Get the User Email_key for a certain user:
SELECT Email_key From User_Confirmation WHERE username='TheDoctor'

General
UIusername='TheDoctor'
SELECT Email_key From User_Confirmation WHERE username= UIusername
DELETE FROM User_Confirmation WHERE username= UIusername
 Insert general:
UIemail: 'testsubject6@gmail.com'
UIusername: 'BlackList'
INSERT INTO `User_Confirmation`(`user_confirmationID`, `username`, `email`, `Email_key`) 
SELECT UUID(), username, UIemail, UUID()
FROM User
WHERE username= UIusername
Group
group_id: Primary key. The group_id is used for identifying each group. Data type is varchar of size 10() and is unique for each group.
user_id: (foreign key) The user_id is used to identify which user created the group. Data type is varchar of size 10
group_creator: The username of the staff that created the group. Data type is character of size 20 and is unique to each user.
group_name: The name of the group. Data type varchar 50 and is unique for each group and is unique for each group.
Date_created: Date in which the group was created. Data type is current_timestamp of format mm/dd/yyhh:mm:ss.

CREATE TABLE `Create_Group` (
  `group_id` varchar(10) NOT NULL,
  `user_id` varchar(10) NOT NULL,
  `group_creator` varchar(20) NOT NULL,
  `group_name` varchar(50) NOT NULL,
  `date_created` datetime DEFAULT NULL,
   PRIMARY KEY (`group_id`),
   FOREIGN KEY (`user_id`) REFERENCES User(user_id)),
   CONSTRAINT UC_Group UNIQUE (group_id,group_name)
   UNIQUE(group_name)
) ENGINE=InnoDB DEFAULT CHARSET=latin1;

INSERT INTO `Create_Group` (`group_id`, `user_id`, `group_creator`, `group_name`, `date_created`) 
SELECT UUID(),user_id, username,'HeroesUnited', CURRENT_TIMESTAMP()
FROM User
WHERE username='TheDoctor' AND user_type='Staff'

INSERT INTO `Create_Group` (`group_id`, `user_id`, `group_creator`, `group_name`, `date_created`) 
SELECT UUID(),user_id, username,'Vigilantes', CURRENT_TIMESTAMP()
FROM User
WHERE username='BlackList' AND user_type='Staff'

Queries (Example): 

See The information of a group by Group Creator:
SELECT * FROM Create_Group WHERE group_creator='TheDoctor'

See The information of a group by Group name:
SELECT * FROM Create_Group WHERE group_name='HeroesUnited'

Queries (General): 

See The information of a group by Group Creator:
UsernameInput="TheDoctor"

SELECT * FROM Create_Group WHERE group_creator= UsernameInput

See The information of a group by Group name:
UsernameInput='HeroesUnited'

SELECT * FROM Create_Group WHERE group_name= UsernameInput

Insert General:
UIusername='TheDoctor'
UIGroupName='HeroesUnited'

INSERT INTO `Create_Group` (`group_id`, `user_id`, `group_creator`, `group_name`, `date_created`) 
SELECT UUID(),user_id, username, UIGroupName, CURRENT_TIMESTAMP()
FROM User
WHERE username= UIusername AND user_type='Staff'

Group_Permission
permission_id: Primary key. The permmision_id is used for identifying each permission. Data type is varchar of size 10 and is unique for each group permission.
group_id: (foreign key). The group_id is used for identifying which group the user has permission to participate in. Data type is varchar of size 10 and is unique for each group.
username:The username to identify what user has the permission. Data type is character of size 20 and is unique to each user.
permission_creator: The username of the staff that created the permission. Data type is character of size 20 and is unique to each user.
group_name: The name of the group. Data type varchar 50 and is unique for each group and is unique for each group.

CREATE TABLE `Group_Permission` (
 `permission_id` varchar(10) NOT NULL,
 `group_id` varchar(10) NOT NULL,
 `username` varchar(20) NOT NULL CHECK username IN User(username) ,
 `permission_creator` varchar(50) NOT NULL,
 `group_name` varchar(50) NOT NULL,
  PRIMARY KEY (`permission_id`),
  KEY (`group_id`),
   UNIQUE (permission_id)
) ENGINE=InnoDB DEFAULT CHARSET=latin1;


INSERT INTO `Group_Permission` (`permission_id` ,`group_id`, `username`, `permission_creator` ,`group_name`) 
SELECT UUID(), group_id, 'FlashMaster', 'TheDoctor', Create_Group.group_name
FROM Create_Group, User
WHERE Create_Group.group_name= 'HeroesUnited' AND Create_Group.group_creator='TheDoctor' AND User.username='FlashMaster'


INSERT INTO `Group_Permission` (`permission_id` ,`group_id`, `username`, `permission_creator` ,`group_name`) 
SELECT UUID(), group_id, 'Vibe', 'TheDoctor', Create_Group.group_name
FROM Create_Group, User
WHERE Create_Group.group_name= 'HeroesUnited' AND Create_Group.group_creator='TheDoctor' AND User.username='Vibe'


INSERT INTO `Group_Permission` (`permission_id` ,`group_id`, `username`, `permission_creator` ,`group_name`) 
SELECT UUID(), group_id, 'JessiJones', 'TheDoctor', Create_Group.group_name
FROM Create_Group, User
WHERE Create_Group.group_name= 'HeroesUnited' AND Create_Group.group_creator='TheDoctor' AND User.username='JessiJones'

INSERT INTO `Group_Permission` (`permission_id` ,`group_id`, `username`, `permission_creator` ,`group_name`) 
SELECT UUID(), group_id, 'DoctorStrange', 'TheDoctor', Create_Group.group_name
FROM Create_Group, User
WHERE Create_Group.group_name= 'HeroesUnited' AND Create_Group.group_creator='TheDoctor' AND User.username='DoctorStrange'

INSERT INTO `Group_Permission` (`permission_id` ,`group_id`, `username`, `permission_creator` ,`group_name`) 
SELECT UUID(), group_id, 'JessiJones', 'BlackList' , Create_Group.group_name
FROM Create_Group, User
WHERE Create_Group.group_name= 'Vigilantes' AND Create_Group.group_creator='BlackList' AND User.username='JessiJones'

INSERT INTO `Group_Permission` (`permission_id` ,`group_id`, `username`, `permission_creator` ,`group_name`) 
SELECT UUID(), group_id, 'IronFist', 'BlackList' , Create_Group.group_name
FROM Create_Group, User
WHERE Create_Group.group_name= 'Vigilantes' AND Create_Group.group_creator='BlackList' AND User.username='IronFist'


INSERT INTO `Group_Permission` (`permission_id` ,`group_id`, `username`, `permission_creator` ,`group_name`) 
SELECT UUID(), group_id, 'DareDevil', 'BlackList' , Create_Group.group_name
FROM Create_Group, User
WHERE Create_Group.group_name= 'Vigilantes' AND Create_Group.group_creator='BlackList' AND User.username='DareDevil'


INSERT INTO `Group_Permission` (`permission_id` ,`group_id`, `username`, `permission_creator` ,`group_name`) 
SELECT UUID(), group_id, 'Samuroid', 'BlackList' , Create_Group.group_name
FROM Create_Group, User
WHERE Create_Group.group_name= 'Vigilantes' AND Create_Group.group_creator='BlackList' AND User.username='Samuroid'

INSERT INTO `Group_Permission` (`permission_id` ,`group_id`, `username`, `permission_creator` ,`group_name`) 
SELECT UUID(), group_id, 'TEST123', 'DareDevil' , Create_Group.group_name
FROM Create_Group, User
WHERE Create_Group.group_name= 'Vigilantes' AND Create_Group.group_creator='DareDevil' AND User.username='TEST123'

INSERT INTO `Group_Permission` (`permission_id` ,`group_id`, `username`, `permission_creator` ,`group_name`) 
SELECT UUID(), group_id, User.username, 'DareDevil' , Create_Group.group_name
FROM Create_Group, User
WHERE Create_Group.group_name= 'Vigilantes' AND Create_Group.group_creator='BlackList' AND User.username='TEST123'











Queries: 

See all the users in a group (full info):
SELECT * FROM Group_Permission  WHERE group_name='HeroesUnited'


See all the users in a group (username only):
SELECT username FROM Group_Permission  WHERE group_name='HeroesUnited'

General:
UsernameInput='HeroesUnited'

See all the users in a group (full info):
SELECT * FROM Group_Permission  WHERE group_name= UsernameInput

See all the users in a group (username only):
SELECT username FROM Group_Permission  WHERE group_name= UsernameInput

Insert General:

UIusername='Samuroid'
UIpermission_creator='BlackList'
UIgroup_name='Vigilantes'

INSERT INTO `Group_Permission` (`permission_id` ,`group_id`, `username`, `permission_creator` ,`group_name`) 
SELECT UUID(), group_id, UIusername, UIpermission_creator, Create_Group.group_name
FROM Create_Group, User
WHERE Create_Group.group_name= UIgroup_name AND Create_Group.group_creator= UIpermission_creator AND User.username= UIusername



























Question 
question_id: Primary key. The question_id is used for identifying each unique question. Data type is varchar of size 10and is unique for each question.
user_id: (foreign key) The user_id is used to identify the staff that created the question. Data type is varchar of size 10.
group_name: The name of the group that presented the question for vote. Data type varchar 50 and is unique for each group and is unique for each group.
question_creator: The question_creator is the username of the staff that posted the question. Data type is character of size 20 and is unique to each user.
question_type: The question_type is used for identifying what type of question will be asked. Data type is character of size 20.
question_title: The question_title is a condensed version of the question asked. Data type is character of size 50.
question_descrition: The question_description is a detailed version of the question asked. Data type is character of size 500.
voting_status: Identifies if the question has yet to be voted on, if the voting is in progress, or if the voting has been done.Data type is character of size 20.
question_author:The question_author issued to determine which user presented the question to the group.  Data type varchar of size 20.
Date_created: Date in which the question was created. Data type is current_timestamp of format mm/dd/yyhh:mm:ss.



CREATE TABLE `Question` (
  `question_id` varchar(15) NOT NULL,
  `user_id` varchar(10) NOT NULL,
  `group_name` varchar(50) NOT NULL,
  `question_creator` varchar(20) NOT NULL,
  `question_type` varchar(20) NOT NULL,
  `question_title` varchar(50) NOT NULL,
  `question_description` varchar(500) NOT NULL,
  `voting_status` varchar(20) ,
  `question_author` varchar(20),
  `date_created` datetime DEFAULT NULL,
   PRIMARY KEY (`question_id`),
   KEY (`user_id`),
   KEY (`group_id`),
   UNIQUE (question_id)
) ENGINE=InnoDB DEFAULT CHARSET=latin1;


INSERT INTO `Question`(`question_id`, `user_id`, `group_name`, `question_creator`, `question_type`, `question_title`, `question_description`, `voting_status`, `question_author`, `date_created`) 
SELECT UUID(),user_id,group_name, group_creator , 'Proposition','Rename the TARDIS','Rename the doctor’s TARDIS','COMPLETED','Jessica Jones', CURRENT_TIMESTAMP()
FROM Create_Group
WHERE group_creator='TheDoctor' 

INSERT INTO `Question`(`question_id`, `user_id`, `group_name`, `question_creator`, `question_type`, `question_title`, `question_description`, `voting_status`, `question_author`, `date_created`) 
SELECT UUID(),user_id,group_name, group_creator , 'Proposition','Destruction of Killgrave','Destruction of Killgrave Description','Completed','Jessica Jones',CURRENT_TIMESTAMP()
FROM Create_Group
WHERE group_creator='TheDoctor' 

INSERT INTO `Question`(`question_id`, `user_id`, `group_name`, `question_creator`, `question_type`, `question_title`, `question_description`, `voting_status`, `question_author`, `date_created`) 
SELECT UUID(),user_id,group_name, group_creator , 'Amendment','Destruction of Killgrave','Destruction of Killgrave Amendment Description','In-Progress','TheDoctor',CURRENT_TIMESTAMP()
FROM Create_Group
WHERE group_creator='TheDoctor'

INSERT INTO `Question`(`question_id`, `user_id`, `group_name`, `question_creator`, `question_type`, `question_title`, `question_description`, `voting_status`, `question_author`, `date_created`) 
SELECT UUID(),user_id,group_name, group_creator, 'Proposition','Destruction of Killgrave','Destruction of Killgrave Description','Completed','Jessica Jones',CURRENT_TIMESTAMP()
FROM Create_Group
WHERE group_creator='Blacklist'

Queries Examples: 
Get all a certain questions info:
SELECT * FROM Question  WHERE question_title='Rename the TARDIS' and question_type='Proposition' and group_name='HeroesUnited'
Get all a current questions info:

SELECT * FROM Question  WHERE voting_status='In-Progress' and group_name='HeroesUnited'

Queries General: 
UIQtitle='Rename the TARDIS'
UIQtype='Proposition' 
UIGroupName='HeroesUnited'

Get all a certain questions info:
SELECT * FROM Question  WHERE question_title=  UIQtitle and question_type= UIQtype and group_name= UIGroupName

Get all a current questions info:
SELECT * FROM Question  WHERE voting_status='In-Progress' and group_name= UIGroupName

Insert General
UIquestion_type='Proposition'
UIquestion_title='Destruction of Killgrave'
UIquestion_description='Destruction of Killgrave Description'
UIstatus='Completed'
UIquestion_author='Jessica Jones'
UIgroup_creator='Blacklist'

INSERT INTO `Question`(`question_id`, `user_id`, `group_name`, `question_creator`, `question_type`, `question_title`, `question_description`, `voting_status`, `question_author`, `date_created`) 
SELECT UUID(),user_id, group_name, group_creator, UIquestion_type, UIquestion_title, UIquestion_description, UIstatus, UIquestion_author ,CURRENT_TIMESTAMP()
FROM Create_Group
WHERE group_creator= UIgroup_creator



Voting 
voting_ID: Primary key. Used for identifying each unique voting. Data type is varchar of size 20.
question_ID: (foreign key)Used to identify which user is creating the meeting. Data type is varchar of size 10.
group_name: The name of the group that presented the question for vote. Data type varchar 50 and is unique for each group and is unique for each group.
question_creator: The question_creator is the username of the
question_title: A condensed version of the question asked. e question has yet to be voted on, if the voting is in progress, or if the voting has been done. Data type is character of size 50.
question_type: The question_type is used for identifying what type of question will be asked. Data type is character of size 20.
voting_choice: The choice that the user chooses for the given question. The votes can be yes, no, or abstained. Data type is character of size 9. 

CREATE TABLE `Voting` (
  `voting_id` varchar(20) NOT NULL,
  `question_id` varchar(10) NOT NULL,
  `group_name` varchar(50) NOT NULL,
  `question_title` varchar(50) NOT NULL,
  `question_type` varchar(20) NOT NULL,
  `voting_choice` varchar(9) NOT NULL,
   PRIMARY KEY (`voting_id`),
   KEY (`question_id`),
   UNIQUE (voting_id)
) ENGINE=InnoDB DEFAULT CHARSET=latin1;

(x4 with different votes)
INSERT INTO `Voting` (`voting_id`, `question_id`, `group_name` ,`question_title`, `question_type` ,`voting_choice`) 
SELECT UUID(),question_id, group_name , question_title, question_type,'No'
FROM Question
WHERE  question_title='Rename the TARDIS' AND group_name='HeroesUnited' AND question_type='Proposition'
(x4 with different votes)
INSERT INTO `Voting` (`voting_id`, `question_id`, `group_name` ,`question_title`, `question_type` ,`voting_choice`) 
SELECT UUID(),question_id, group_name , question_title, question_type,'No'
FROM Question
WHERE  question_title='Destruction of Killgrave' AND group_name='HeroesUnited' AND question_type='Proposition'
(x4 with different votes)
INSERT INTO `Voting` (`voting_id`, `question_id`, `group_name` ,`question_title`, `question_type` ,`voting_choice`) 
SELECT UUID(),question_id, group_name , question_title, question_type,'No'
FROM Question
WHERE  question_title='Destruction of Killgrave' AND group_name='HeroesUnited' AND question_type='Amendment'
(x4 with different votes)
INSERT INTO `Voting` (`voting_id`, `question_id`, `group_name` ,`question_title`, `question_type` ,`voting_choice`) 
SELECT UUID(),question_id, group_name , question_title, question_type,'No'
FROM Question
WHERE  question_title='Destruction of Killgrave' AND group_name='Vigilantes' AND question_type='Proposition'





Queries:
See how many Yes there where:
SELECT COUNT(voting_choice) FROM Voting  WHERE group_name='Vigilantes'  AND question_title='Destruction of Killgrave'  AND question_type='Proposition' AND voting_choice='Yes'

DELETE (WARNING MUST DELETE ALL THE VOTES IFF THE RESULTS WHERE SAVED IN TABLE RESULT):
DELETE FROM Voting WHERE group_name='Vigilantes' AND question_title='Destruction of Killgrave'  AND question_type='Proposition'

General Votes:
UIgroupname='Vigilantes' 
UIquestion_title='Destruction of Killgrave'
UIquestion_type='Proposition' 
UIvoting_choice='Yes' OR ‘No’ OR ‘Abstain’
SELECT COUNT(voting_choice) FROM Voting  WHERE group_name= UIgroupname AND question_title= UIquestion_title  AND question_type= UIquestion_type AND voting_choice= UIvoting_choice

General insert
INSERT INTO `Voting` (`voting_id`, `question_id`, `group_name` ,`question_title`, `question_type` ,`voting_choice`) 
SELECT UUID(),question_id, group_name , question_title, question_type, UIvoting_choice
FROM Question
WHERE  question_title= UIquestion_title AND group_name= UIgroupname AND question_type= UIquestion_type

General Delete:

DELETE FROM Voting WHERE group_name= UIgroupname AND question_title= UIquestion_title  AND question_type= UIquestion_type



















Result
result_ID:  Primary key. Used for identifying each unique result. Data type is varchar of size 10.
question_ID: (foreign key)Used to identify which question the result if from. Data type is varchar of size 10.
question_title: A condensed version of the question asked. e question has yet to be voted on, if the voting is in progress, or if the voting has been done. Data type is character of size 50.
total_voters: Total number of users that have voted for a given question. Data type is an integer of 3 digits.
count_yes: Total number of users that voted yes for a given question. Data type is an integer of 3 digits.
count_no: Total number of users that voted no for a given question. Data type is an integer of 3 digits.

CREATE TABLE `Results` (
 `result_id` varchar(10) NOT NULL,
 `question_title` varchar(50) NOT NULL,
 `question_type` varchar(20) NOT NULL,
 `group_name` varchar(50) NOT NULL,
 `count_yes` int(3),
 `count_no` int(3),
 `count_abstain` int(3), 
 `total_voters` INT(3) ,
  PRIMARY KEY (`result_id`),
  UNIQUE (result_id)
) ENGINE=InnoDB DEFAULT CHARSET=latin1;


INSERT INTO `Results`(`result_id`, `question_title`, `question_type`, `group_name`, `count_yes`, `count_no`, `count_abstain`, `total_voters`) 
VALUES 
(UUID(),'Rename the TARDIS' ,'Proposition','HeroesUnited', 1,3,0,4);

INSERT INTO `Results`(`result_id`, `question_title`, `question_type`, `group_name`, `count_yes`, `count_no`, `count_abstain`, `total_voters`) 
VALUES 
(UUID(),'Destruction of Killgrave','Proposition','HeroesUnited', 1,3,0,4);

INSERT INTO `Results`(`result_id`, `question_title`, `question_type`, `group_name`, `count_yes`, `count_no`, `count_abstain`, `total_voters`) 
VALUES 
(UUID(),'Destruction of Killgrave','Amendment','HeroesUnited', 1,1,2,4);

INSERT INTO `Results`(`result_id`, `question_title`, `question_type`, `group_name`, `count_yes`, `count_no`, `count_abstain`, `total_voters`) 
VALUES 
(UUID(),'Destruction of Killgrave', 'Proposition','Vigilantes', 3,0,1,4);


Queries:
Everything from Results:
SELECT * FROM Results WHERE question_title='Destruction of Killgrave' AND question_type='Proposition' AND group_name='Vigilantes'
General:
UIgroupname='Vigilantes'
UIquestion_title='Destruction of Killgrave'
UIquestion_type='Proposition'
SELECT * FROM Results WHERE question_title= UIquestion_title AND question_type= UIquestion_type AND group_name= UIgroupname

Yes/No/Abstain:

SELECT count_yes FROM Results WHERE question_title= UIquestion_title AND question_type= UIquestion_type AND group_name= UIgroupname
SELECT count_no FROM Results WHERE question_title= UIquestion_title AND question_type= UIquestion_type AND group_name= UIgroupname
SELECT count_abstain FROM Results WHERE question_title= UIquestion_title AND question_type= UIquestion_type AND group_name= UIgroupname



Insert general:
UIgroupname='Vigilantes'
UIquestion_title='Destruction of Killgrave'
UIquestion_type='Proposition'

QIyes=SELECT COUNT(voting_choice) FROM Voting  WHERE group_name= UIgroupname AND question_title= UIquestion_title  AND question_type= UIquestion_type AND voting_choice= 'Yes'
QIno=SELECT COUNT(voting_choice) FROM Voting  WHERE group_name= UIgroupname AND question_title= UIquestion_title  AND question_type= UIquestion_type AND voting_choice= ‘No’
QIabstain=SELECT COUNT(voting_choice) FROM Voting  WHERE group_name= UIgroupname AND question_title= UIquestion_title  AND question_type= UIquestion_type AND voting_choice= ‘Abstain’
QIvoters=SELECT COUNT(username) FROM Group_Permission WHERE group_name= UIgroupname



INSERT INTO `Results`(`result_id`, `question_title`, `question_type`, `group_name`, `count_yes`, `count_no`, `count_abstain`, `total_voters`) 
VALUES 
(UUID(),UIquestion_title, UIquestion_type, UIgroupname, QIyes, QIno, QIabstain, QIvoters);






1)Testing 
1. fixed if 2 diffrent groups asked the same question that the votes didnt merge
2. fixed that if there are 2 same question but with diffrent types that it does not merge the example ammendment to the proposition.
3. fixed that all ids and usernames would be unique
4. made sure that if the group doesent exist then the question would not be placed in the database
5.made sure that only admins can create group. If a user tries to make a group it is not inserted in the database.
6. The date is automated so the user can not ‘Fake’ a date.
7. Made sure that the staff is the only one that can create permissions to join the group.
8.Made sure that the name of the group is unique
9.Made the select a lot less complicated
10. Fixed resuts so it would be connected to a group instead of a question just in case 2 groups have a question with a similar name
11. Added question type to results just in case there is an ammendment ext.
12. Added user confirmation table
13.fixed atrribute in user confirmation table(key to Email_key)
14. turned all queries to a more general format (variables instead of Uiuser)
15. Added Deleted to voting and group_permission



