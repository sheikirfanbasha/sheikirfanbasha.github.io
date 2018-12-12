---
layout: post
title: Moodle Plugin - Course Completed Enrolment
image: assets/images/moodle-enrol-course.jpg
featured: true
hidden: false
author: sheikirfanbasha
categories: [ moodle, enrol_coursecompleted, plugin, lms ]
---

Moodle is a learning platform designed to provide educators, administrators and learners with a single robust, secure and integrated system to create personalised learning environments.

`enrol_coursecompleted` is a plugin for moodle that allows to create a chain of courses. After completion of a course, the student is automatically enrolled in one or more other courses. But it is also possible to give a user another role in the same course when he/she completes the course.

Though this plugin is quite useful, it is very tricky to get it working. Hence, this post explains in detail about the steps required to get this plugin fully functional.

Let's get started!

### Prerequisites

- [Downlaod](https://download.moodle.org/) and install moodle

- [Download](https://moodle.org/plugins/enrol_coursecompleted) the `enrol_coursecompleted` plugin

### 1. Install the plugin

- Login as admin

   - > Site administration -> Plugins(tab) -> Install plugins -> choose file -> Install plugin from zip file

- Make sure you upgrade the database once the plugin is installed

- Test

	- `mysql` binary will be usually located in `<installaed_root_dir>/Library/bin`

		- > select * from mdl_config_plugins where plugin='enrol_coursecompleted';
 	  

### 2. Enable the plugin
	
- > Site administration -> Plugins(tab) -> Plugins overview -> Enrolment methods settings (refer image below) -> Enable plugin (refer image below) 

![plugin-enrolment-methods]({{site.baseurl}}/assets/images/plugin-enrolment-methods.png)

![enable-plugin]({{site.baseurl}}/assets/images/enable-plugin.png)


### 3. Enable course completion tracking

- > Site administrator -> Advanced features -> Enable completion tracking (select checkbox)

![enable-course-completion]({{site.baseurl}}/assets/images/enable-course-completion.png)

### 4. Create course

- While creating a course, make sure you choose the `completion tracking` choice as `yes`. This is important to enable course completion settings for this course.

![course-completion-track-enable]({{site.baseurl}}/assets/images/course-completion-track-enable.png)

### 5. Create activity

- While creating an activity, make sure you have set the activity completion criteria as per your preference.

![activity-completion]({{site.baseurl}}/assets/images/activity-completion.png)


### 6. Edit course completion settings

- Ensure you edit the course completion criteria as per your preference

![course-completion-setting]({{site.baseurl}}/assets/images/course-completion-setting.png)

![course-completion-criteria]({{site.baseurl}}/assets/images/course-completion-criteria.png)

### 7. Set the enrolment setting

- Using course settings, set the preference for the users to enrol for the course. Make sure you move the prefered enrolment method to the top(using the arrow buttons) in the list and disable the other enrolment options which you think are not applicable.


![course-enrol-setting]({{site.baseurl}}/assets/images/course-enrol-setting.png)

![enrolment-option]({{site.baseurl}}/assets/images/enrolment-option.png)

![set-enrolment-method]({{site.baseurl}}/assets/images/set-enrolment-method.png)


### 8. Create another course

- Create another course which you want to chain with the above course.

### 9. Set the enrolment setting to `course completed enrolement`

- > Course settings -> more ->  users(tab) -> Enrolment methods -> Select course completed enrolment(using choice box) -> choose the course that you want to chain with -> save the changes

Make sure you move the `course completed enrolement` enrolment method to the top(using the arrow buttons) in the list and disable the other enrolment options which you think are not applicable.

![new-enrolment-option]({{site.baseurl}}/assets/images/new-enrolment-option.png)

![new-enrolment-setting]({{site.baseurl}}/assets/images/new-enrolment-setting.png)

![new-enrolment-final]({{site.baseurl}}/assets/images/new-enrolment-final.png)


### 10. Test

- Create a new user
	- > Site administrator -> Users(tab) -> add new user (under Accounts) -> set password
- Login as new user
- Enrol for the first course and complete it
- Login as admin user and maually trigger the cron job which saves the completed courses state in database
	- > http://localhost:8888/moodle36/admin/cron.php?password=opensesame
- Wait for 1-2 minutes and login with new user. Now, you shall see that you are automatically enrolled for the second course.

### Tip

Few of the moodle database tables that come handy to debug in case of issues are:

- `mdl_course_modules`  

- `mdl_course_modules_completion` 

- `mdl_course_completion_criteria`

- `mdl_course_completion_aggr_method`

- `mdl_course_completions`

Please feel free to comment in case of any issues.