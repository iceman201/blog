---
layout: post
title:  "GymWorkOut Application Project"
date:   2016-07-08
excerpt: "Project blog"
project: true

tag:
- project
comments: false
---

# Gym workout manager

**iOS Application** / **Swift2.2** / **Xcode7.3**

## Why?
Reason of creating this application is really simple, “I need it” I have been use a lot app for manager workout, even some powerful app like iHealth(iOS), Google Fit(Android), and sHealth(Android). They all powerful application, but it may be bit over. For myself, I don't want to wasting time on the gym, I need more focus to carry out my plan. If an application could do the basic work and it has very simple interaction, that would solve my problem.

## Whats inside?
Basic design of the application is separate to 4 part, **Timer**, **Record**,**Profile**,**Analysis**.

* Timer
	* provide some 3 way of time recording method which coved “cardio workout” and “weights workout”. Inside of the Timer view controller, it has a *claim* button which for user record what exercise he/she has done.

<figure class="third">
	<img src="/assets/blogImages/timer.png">
	<img src="/assets/blogImages/timer2.png">
	<img src="/assets/blogImages/timer3.png">
	<figcaption>Basically user could setup workout type and Set time & Reset.</figcaption>
</figure>

* Record
	* display which type of workout and what exercise you have done.

<figure class="half">
	<img src="/assets/blogImages/record.png">
	<img src="/assets/blogImages/record2.png">
	<figcaption>For user checking what exercise they have done and delete record.</figcaption>
</figure>

* Profile
	* User enter their basic information in the local database such as weights and height, thats for further analysis.
	* BMI/BMR body fat calculator * *may connect to physical device for body fat percentage detect in future version*
	* Calendar for setup workout plan by chosen date.

<figure class="half">
	<img src="/assets/blogImages/profile.png">
	<img src="/assets/blogImages/BMI.png">
	<figcaption>For user checking what exercise they have done and delete record.</figcaption>
</figure>	

<figure class="third">
	<img src="/assets/blogImages/plan.png">
	<img src="/assets/blogImages/calendar.png">
	<img src="/assets/blogImages/setplan.png">
	<figcaption>For user checking what exercise they have done and delete record.</figcaption>
</figure>	

* Analysis
	* Design work is yet to come, main idea for this part is use the data of Realm that user entered and doing some graphic analysis. So far only done one part which is to showing user some direction of workout, for instance the pie chart of showing percentage of workout type, like 85% weights 10% cardio 5% Hiit. Hence user may consider something like "hm.. Maybe too much weights? as for get a good body sharp might be bit balence out my plan?"
