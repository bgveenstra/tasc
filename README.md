
# TASC - Teachers And Students Connecting
[Heroku Link](https://floating-lowlands-88571.herokuapp.com/)

#### Sample Logins:

##### Student Account
- email: GA@student.com
- password: GAisnum1

##### Teacher Account:
- email: GA@student.com
- password: GAisnum1

#### Elevator Pitch:
We asked ourselves, how hard could it be to make something better than Schoology that provides the same Schoology functionality, but with a better user experience and also was the location for all regular homework assignment and project completion?  We took it upon ourselves to look for a real world problem we faced and try to solve it.  We learned a whole lot in the process!

[Task Tracking](https://github.com/Vedelopment/learning-hub/projects/1)

### Technologies:
Ruby
Rails
Materialize
JavaScript
Jquery
Bcrypt
client_side_validations
Github API

### Wish List:
Teacher to teacher feedback
Student to teacher pulse checks
Teacher to student feedback
Emails
Attendence tracking
Friendly URLs
Slack notifier
Chron Job

### Contributors:
* LD - https://github.com/Vedelopment
* Michael - https://github.com/mblair415
* Ricardo - https://github.com/ricarellano
* RJ - https://github.com/johnson-rl

### Flexible Technical Requirements:
Authentication & Authorization
External API
Additional Associations

### Further Exploration:
Sessions

## Who is our user

All of us!  

We find that the most imporatant use of our site is that the most relevant information is easy to access and that communication flows freely.

### Teachers

* teachers can create assignments - like creating a homework assignment.
* teachers can create feedbacks on submissions - like providing feedback on homework.
* teachers can look at all assignments and all submissions - like looking at all homework assignments and all homework submissions from all students. 

### Students

* students can create submissions on released assignments - like turning in homework on an assigned assignment.
* students can view released assignments and their own submissions - like looking at assigned homework and the same student’s responses.
* students can view feedback provided by teachers on that student’s submissions - students can only see feedback given to them

![wireframes one](https://i.imgur.com/gqRqpas.jpg)

## Code we are proud of

### Ricardo
```
def self.get_profile_pic(student)
    student.profile_image = Student.get_github_img (student.github)
    student.save
  end
  def self.get_github_img (github_user)
    if github_user.include? "http"
      github_username = Student.parse_github_username(github_user)
    elsif github_user == ""
      github_username = "image"
    else
      github_username = github_user
    end
    response = HTTParty.get('https://api.github.com/users/' + github_username)
    return response["avatar_url"]
  end
  def self.parse_github_username (github_url)
    temp_array = github_url.split('/')
    username = temp_array[temp_array.length - 1]
    return username
  end
end
```
### Mike
```
<div>
      <% if current_student == @submission.student %>
        <div class="col s12 center">
          <%= link_to "Edit Submission", edit_submission_path(@submission), class:"waves-effect btn waves-light form-submit-style" %>
        </div>
      <% end %>
    </div>
  <% end %>
</div>
</div>
<div class="row">
<% if current_teacher %>
  <div class="col m9 offset-m1 form form-style">
    <h4 class="center">Homework Feedback</h4>
    <% if @submission.feedback %>
      <%= @submission.feedback.content %>
      <div class="center">
        <%= link_to "Edit Feedback", edit_feedback_path(@submission.feedback), class:"waves-effect btn waves-light form-submit-style" %>
      </div>
    <% else %>
      <div class="center">
        <%= link_to "Provide Feedback", new_feedback_path(@submission), class:"waves-effect btn waves-light form-submit-style" %>
      </div>
    <% end %>
  </div>
<% end %>
<br><br>
</div>
```
### LD

#### D3

```
  var viz = function(dataset){
    d3.select("#graphBar").selectAll("div")
      .data(dataset)
      .enter()
      .append("div")
      .attr("class", "bar")
      .style("height", function(d) {
          var barHeight = d * 20;  //Scale up by factor of 5
          return barHeight + "px";
    });
```
#### Polymorphic Relationships
```
class Student < ApplicationRecord
  has_many :student_courses
  has_many :courses, through: :student_courses
  has_many :submissions
  has_many :feedbacks, as: :communication
  has_many :assignments, through: :submissions
Add Comment Collapse
```

### Ryan
```
<!-- Determines if submitted -->
                  <p class="col m1"> <!-- This <p> must remain BEFORE the if -->
                    <% if @submissions.find_by({assignment_id: a.id}) && @display %>
                    <i class="tiny material-icons">done</i>
                  </p>
                  <!-- Feedback if provided -->
                  <p class="col m3">
                    <% if @submissions.find_by({assignment_id: a.id}).feedback %>
                      <%=link_to "Feedback", feedback_path(@submissions.find_by({assignment_id: a.id}).feedback) %>
                    <% end %>
                    <% end %>
                  </p> <!-- This </p> must come AFTER the end -->
```

## The TASC ERD


![Database ERD](https://i.imgur.com/MW9gotA.png)
