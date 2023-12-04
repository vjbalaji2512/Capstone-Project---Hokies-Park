# Capstone-Project---Hokies-Park

Members -  Vijay Balaji, Manas Shukla, Preyas Hanche, Vrajesh Shah, Arwa Alebrahim, Anupa Shah 

# DEMO

The link to the narrated demo is as follows:
https://drive.google.com/file/d/1ZDeHV8vSbxnf2wTG-0K7NW_6_1Vun83k/view?usp=sharing

# INTRODUCTION

Currently, there are plenty of parking lots and vacant spots available for vehicles in the campus area, and a lot of people are not aware of their whereabouts and how empty they tend to be on different days. There’s no system in place to perform this task efficiently, and people face this problem frequently, especially during big events like match days and festivals.
For the scope of this project, the preliminary focus was on generating and leveraging data for parking lots on campus to provide vacancies, followed by an analysis of the history data provided by parking team to optimize business decisions, and an Image processing prototype to track parking spaces using a live video feed. Along with this, we also provided functionality to users who sell parking spaces in their driveways during game days, so others can book them digitally.

# PRODUCT FUNCTIONALITIES
The Project consists of 6 main functionalities – Login/Register, Finding Parking Vacancies, Adding an Independent Parking for sublease, Booking an Independent Parking for sublease, Data Analysis, and Finding Vacancies through live feed. They are detailed as below:


1.	Login/Register
By clicking on the ‘Login’ Option from the navigation menu, users can log in to, and log out of the portal. The login and Registration forms, both have input validations.

![image](https://github.com/vjbalaji2512/Capstone-Project-Hokies-Park/assets/124394195/14518ed7-526c-404a-ae2d-647bea2090fa)

After Logging in, the Name of the logged-in user is displayed on the navigation bar.

![image](https://github.com/vjbalaji2512/Capstone-Project-Hokies-Park/assets/124394195/5955d127-aad6-4e72-9fe8-f6c5fa591e90)

2.	Finding Parking Vacancies
Users can find how much vacancy each parking lot on campus has by clicking on ‘Find a Parking’ as shown below:
![image](https://github.com/vjbalaji2512/Capstone-Project-Hokies-Park/assets/124394195/0710fa0c-a1fa-4f62-bf94-94aebcd8253c) 


The Parking lots with their vacancies are displayed below: 
![image](https://github.com/vjbalaji2512/Capstone-Project-Hokies-Park/assets/124394195/e4bb818e-5055-4133-a55f-485311527957)


The Parking Management can modify vacancies at the Backend using simple API calls such as updateLot/lotVacancy/ebafe10f-1bdd-49e6-9af2-8280a0d899e6/25
The call above sets the vacancy for Owen Parking Lot as 25, which is revealed to the users on clicking the update button
 
![image](https://github.com/vjbalaji2512/Capstone-Project-Hokies-Park/assets/124394195/813296f2-b7ea-41c1-bcb1-2873a8077a11)

3.	Adding an Independent Parking for sublease
	The Independent Parking Sublease can be added through the form provided in the ‘Quick Links’ section for the same.
 ![image](https://github.com/vjbalaji2512/Capstone-Project-Hokies-Park/assets/124394195/3c27d4ec-c436-4a8f-8763-ede9134825f2)

By clicking the Submit button, the sublease data can be added for a logged-in user.

4.	Booking an Independent Parking for sublease
Similarly, ‘Book a Parking’ enables logged-in users to view subleases posted by other logged-in users. They can click the Book Now button to finalize the Booking

![image](https://github.com/vjbalaji2512/Capstone-Project-Hokies-Park/assets/124394195/f94a9906-cb43-4282-a26f-04e6fe7f3ab2)

The bookings can be viewed using the My Bookings option on the nav bar

![image](https://github.com/vjbalaji2512/Capstone-Project-Hokies-Park/assets/124394195/91c93b7a-a780-4197-9b03-072ea21c4c9d)

5.	Data Analysis
The team also received some historical data for the ‘North-End Center’ parking lot for the year 2021 and analyzed the same. Some Interesting information revealed by the analysis is as follows:

![image](https://github.com/vjbalaji2512/Capstone-Project-Hokies-Park/assets/124394195/f7631bf3-33f5-4880-a20f-37fb3ad215e3)

![image](https://github.com/vjbalaji2512/Capstone-Project-Hokies-Park/assets/124394195/52beb476-34cb-4a8c-9441-14cfd242dd74)

(The revenue obtained monthly throughout the year)

![image](https://github.com/vjbalaji2512/Capstone-Project-Hokies-Park/assets/124394195/95dd9da1-8da1-4ff2-9dd4-c72dd95bc7e2)

(The usage of permits in the lot over the year)

6.	Finding Vacancies through a live feed
A demo video prototype was built by the team to evaluate a live stream video and find vacant parking spots in the stream. The working of the prototype is also detailed in the narrated demo. The counter of vacancies can be seen on the top-left corner of the running feed.

![image](https://github.com/vjbalaji2512/Capstone-Project-Hokies-Park/assets/124394195/5fef52a9-8eb2-43c0-b789-71894e1583c8)

# DESIGN

The Overview of the System Design for the Entire Application is as below:

![image](https://github.com/vjbalaji2512/Capstone-Project-Hokies-Park/assets/124394195/2f133636-3654-48a6-a541-e6c6173d2e27)

The Design is Split into 3 major portions – Web Portal, Data Analysis, and Image Processing.

1.	Web Portal
The Web Portal uses a DynamoDB backend, Springboot APIs to access the backend, and an HTML/CSS/JS design for the interface accessed by the users. The reason why DynamoDB was chosen was the fact that it provides with scalability, availability and flexibility. The database is always available on the cloud and goes by a pay-per-use cost structure. This way, future development can analyze the cost of scaling the product easily. The flexibility it provides is that anyone can create an account for Amazon Web Services, and use the database through an IAM role for the database. This way, if the application was to be extended, different parking lot owners can create their own database, and share the IAM role key with the developer team to connect it to the portal. This way, any number of parking lots can be added to the portal from different vendors at any time. Since the database is hosted on the cloud, it saves server space for database storage as well.

The Springboot controller provides an easy way to access the database through APIs. To create, read or update any parking lot, user or bookings, a simple API call shall suffice. This abstracts the need of any backend logic into the controller code. This also adds to the flexibility of the product. If any vendor wants to use their database instead of DynamoDB, the controller can also be set up to call that particular database and expose APIs for the same to the fronted interface and vendor management alike. This functionality was implemented keeping in mind that in the future, vendors such as the VT Parking team would want to connect their services to create and modify the parking lots and their vacancies.

The controllers are abstracted from the databases using a repository design pattern. The controllers can access the database by making use of DAOs (Data Access Objects). This way, if the backend is changed from DynamoDB to MySQL in the future, only the logic for the repository will change, without the need for a change in logic in any other part of the application. This also enabled the developers to easily handle unit tests, as there was no need to access the databases to test the controllers. 

The data of the users is encrypted on the backend by the use of the Crypto module of SpringBoot. This way, only the users have access to their private data, ie passwords. The Spring Security Crypto module provides support for symmetric encryption, key generation, and password encoding. This implementation uses the widely supported "bcrypt" algorithm to hash the passwords. Bcrypt uses a random 16-byte salt value and is a deliberately slow algorithm, to hinder password crackers.

The data flow diagram for the portal is as below:

![image](https://github.com/vjbalaji2512/Capstone-Project-Hokies-Park/assets/124394195/cdde71ed-17e1-4fba-ab2a-ab0cb52140cc)


2.	Data Analysis
Data Gathered: The data was collected through the VT Parking management system known as PARCS. The service runs on North-End parking garage and obtains each incident of entry and exit, storing it to the backend database. This way, we could obtain the historical data for the last year, and provide insights into it using exploratory analysis techniques. For this task, Jupyter Notebooks were used based on Python, and the use of Pandas, matplotlib, and seaborn allowed us to extract interesting insights from the data and create visualizations. 

Pandas provides excellent data representation, with features to optimally slice and explore the data. It also allows to efficiently handle big data, abstracting the implementation details behind it. This allows analysts to freely explore the data without worrying about complexities. Matplotlib and Seaborn are libraries supporting Python and are efficient for creating data visualizations. This way, the insights can easily be presented to external stakeholders without the need to explain complex and detailed tables. Another advantage is that the libraries are open source, thus free to use for all.

3.	Image Processing
Performing operations on an image to obtain useful information is known as image processing. This field focuses on manipulating digital images with the aid of a computer and develops a computer system capable of processing images. It is a type of signal processing in which an image is the input, and the outcome may be an image or characteristics associated with that image. To perform image processing, we use the OpenCV library provided by Python, mainly focused on real-time computer vision. This can be applied to a variety of areas such as 2D and 3D feature toolkits, facial & gesture recognition, human-computer interaction, and mobile robotics. In terms of computer vision, machine learning, and image processing, OpenCV is a large open-source library that includes many capabilities. It helps in identifying objects, faces, and even handwriting by processing images and videos. With its integration with other libraries, such as Numpy, which is a highly optimized library for numerical operations, it is possible to perform multiple operations on the image or video. Among the advantages of OpenCV is its ability to provide access to more than 2,500 state-of-the-art and classic algorithms. Users can perform various tasks with this library, including removing red eyes, extracting 3D models of objects, and following eye movements.

This project focuses on detecting and assessing the number of vacant parking spaces and the location of those spaces based on the concept of Image Processing using OpenCV. Using surveillance cameras in the parking lot, photos/videos are captured to determine whether car parks are occupied. With this image/video, vacant parking spaces can be identified, and users can check the availability of parking through the web application for Hokies Park. The implementation of this system also can reduce traffic congestion and wasted time.

Data:

To illustrate the real-time parking session, we are using a sample aerial view parking image and a timelapse aerial parking image.

![image](https://github.com/vjbalaji2512/Capstone-Project-Hokies-Park/assets/124394195/918fcbec-df8a-4dfb-a4ce-38d324f765c8) 
(a)	Sample Aerial View Parking  		

![image](https://github.com/vjbalaji2512/Capstone-Project-Hokies-Park/assets/124394195/bd108233-1115-4256-8974-6b8215c381d3)
(b) Aerial Parking Time Lapse

Method

The first step is to create a program that allows us to select and deselect parking spaces. In this instance, the image file is used to select the position of the parking spaces, and the video file is played in a loop in order to determine whether the given parking positions are vacant or not. For storing all the positions of the parking space, we use modules like CV2 and pickle. They assist us in locating parking spaces.

To obtain the dimensions such as height and width of the parking space, we use the C2 functionality ( cv2. rectangle). As a next step, we create a file called police (or position list), which contains all the dimensions of the parking space. Using the MouseClick Method, we can select parking space positions in the form of rectangles and once selected, these positions are automatically added to the poslist. Furthermore, right-clicking on the mouse also deselects the positions, which is then overwritten in the poslist file each time it is modified. As soon as the poslist file has been generated, we import the video using the cv2 Video capture feature and loop it for a few seconds. With the help of pickle.load, we display all the positions of the parking spaces from the poslist file into the video. Now the next step is to determine whether or not each parking space is vacant. This is accomplished by examining the pixel count of each parking position based on its edges and corners. Parking positions with fewer edges and corners indicate no vehicles are present in that area, whereas parking positions with more edges and corners indicate the presence of vehicles. A threshold value is also calculated to determine whether a parking space is vacant. 

As soon as that has been accomplished, we display the live pixel count inside the parking position as and when a vehicle appears within it. The pixel count varies according to the vehicle’s movement within a parking spot.  Based on the pixel count value, we check if a  vehicle is present in a particular position, and if the counter value exceeds the threshold, we will color that position red, indicating the presence of a vehicle. When the counter value is below the threshold value, the position is displayed in yellow, indicating that the vehicle is not present. With a live update, the overall counter space having vacant parking space to the total number of parking spaces is calculated and displayed in the upper left corner of the screen.

# AGILE RETROSPECTION

The entire project followed the law of Agile methodology. After the end of each sprint, the developers got together for a retrospective session and noted what could be improved, and what changes could be made for efficient completion of the project. The primary importance of a Sprint Retrospective is that it allows the team to identify potential pitfalls at an early stage and resolve conflict areas. With retrospectives, agile teams can continuously improve the processes by evaluating ‘what all can be improved’.
The retrospective reports after the 3 different sprints are as follows:

SPRINT 1:
●	We implemented all stories except connecting UI with backend streaming. We have carried forward the remaining tasks to the next sprint.
●	We faced a challenge to test the image processing algorithm as there is no real-time data available. To address this, in the next sprint, we will meet the parking team to get real-time feed from the camera.
●	Another point noted in the retrospective was to deploy the backend Java service on a cloud EC2 instance instead of hosting it locally.
●	In this sprint, we can connect UI with backend APIs and Google Map API.

SPRINT 2
●	Since this sprint mainly dealt with data analysis, the main impediment encountered was during the pre-processing of the data. There was a lot of unprocessed, raw parking data (for a whole year) and we needed to make sense of it.
●	We spoke to the Virginia Tech Parking team and got the knowledge of permits along with the meaning of incidents in the parking data, then cleaned up the data for NaN values. We also One-Hot encoded the data depending on whether an incident related to a transient entry or non-transient entry
●	After this data pre-processing, we needed to standardize the dates to get them into 24-hour formats for our analysis. After the data was cleaned up, the analysis could be done successfully.
●	One of the things that went well, is the frequency of meetings within the team and with VT Parking
●	One of the things that can be improved is to create a continuous deployment pipeline for our data analysis or to generate reports from it programmatically since all the report work was done manually by extracting graphs from the Jupyter Notebooks.
SPRINT 3:
●	The sprint had 6 different user stories, but the time estimate for the sprint was low as a lot of the existing code could be re-used for the completion of these tasks
●	Overall, the team agreed that the sprint planning went well, and the story point estimate for the last sprint did not seem correct as it included multiple stories. However, once the sprint began, the team was able to complete the stories within time.

# FUTURE WORK
The project here is a small-scale effort to highlight how the problem of parking can be solved at the Virginia Tech Campus. Since the technology stack used in the project is scalable and maintainable, one of the main ideas is to generalize the project to include any parking vendors that can be extended across multiple locations. Another enhancement of the work could be to streamline the analysis process for smooth communication between the vendors of the analysis and the team. This could be achieved by having a CI/CD pipeline for analysis requests and report submissions, and both the development team and the vendors could be notified of the status of a report. Another feature that can be added is using a verified payment method, along with approval mechanisms for independent parking lot management. This can be done via email or on the portal itself. There are several ways to refine the functionalities of the project, and it can be achieved without hassle, due to the way the system is designed – The backend, controller, and interface follow the principle of ‘Separation of Concerns’, which is essential to the realization of an MVC architecture. 




