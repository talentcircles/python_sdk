# TalentCircles Python Developer Kit

This library allows developers to integrate a TalentCircles network into their own application through HTTP calls to that
network's REST API endpoints.

<!-- ## Setup -->
Setup is simple and easy with pip. Once you are certain you have Python 2.7
installed, use the following command from your project root:
```
$ pip install talentcircles
```

## Usage
First import TalentCircles from talentcircles.talentcircles
```python
from talentcircles.talentcircles import TalentCircles
```
Then initialize the SDK object:
```python
# Use your Network URL, App ID, and Api Key to connect to your API.
# It is reccomended that this information be kept somewhere in your
# project that is not accessible from the public html directory.
app_id = "romeo-5931c22e4190b"
api_key = "Y1IgDgriOjAo5hKMzZ0RxC"
domain = "mytalentmall.talentcircles.vm"

# Initialize the object
talent_api = TalentCircles(domain, app_id, api_key)
```
Then call any of the functions below to access data on the TalentCircles
network you are accessing. For example,
to get a Job object, call `get_job()` with a job id:
```python
job_id = 7480159
job = talent_api.get_job(job_id)
```

## Functions
### Job Functions
**get_job(INT job_id)** - Get a single Job object for the job posting
identified by job_id
```python
job_id = 7480159
job = talent_api.get_job(job_id)
print(job['job_title'])
```

**get_jobs(LIST job_ids)** - Get multiple Job objects for the job postings
identified by a list of job_ids
```python
job_ids = [7480159, 8773787]
two_jobs = talent_api.get_jobs(job_ids)
for job in two_jobs:
    print(job['job_title'])
```

**get_job_candidates(INT job_id)** - Get a list of matching user objects of
possible candidates for the
job posting identified by job_id
```python
job_id = 7480159
job_candidates = talent_api.get_job_candidates(job_id)
for candidate in job_candidates:
    print(candidate['user']['formatted_name'] + " - Score: "
        + str(candidate['score']))
```

**get_similar_jobs(INT job_id)** - Get a list of job objects with job
postings similar to the
job posting identified by job_id
```python
job_id = 7480159
similar_jobs = talent_api.get_similar_jobs(job_id)
for job in similar_jobs:
    print(job['job']['job_title'] + " - Score: " + str(job['score']))
```

**create_job(DICT new_job_data)** - Post a new Job ad, returns the new
Job object
```python
new_job_data = {
  'job_title':'Extremely Excellent Accountant',
  'available_on':'November 6, 2017',
  'category_id': 1,
  'zipcode':94066,
  'description':'We need someone to teach our other accountants.',
}
new_job = talent_api.create_job(new_job_data)
print(new_job['job_title'])
```

**search_jobs(DICT search_params, INT page, INT results_per_page)** - Get a
list of Job objects from the database, using SPHINX search
```python
search_params = {
    "commitment_levels":1
}
page = 1;
results_per_page = 10;
searched_jobs = talent_api.search_jobs(search_params, page, results_per_page)
for job in searched_jobs:
    print(job['job']['job_title'] + " - Score: " + str(job['score']))
```

**update_job(INT job_id, DICT update_data)** - Update an existing job posting
identified by job_id, returns an updated Job object
```python
job_id = 8698598
update_job_data = {
    'job_title':'Very Competent Accountant II'
}
updated_job = talent_api.update_job(job_id, update_job_data)
print(updated_job['job_title'])
```

### User Functions
**get_user(INT user_id)** - Get a single User object for the user profile
identified by user_id
```python
user_id = 12770260
user = talent_api.get_user(user_id)
print(user['firstname'])
```

**get_users(LIST user_ids)** - Get a list of User objects for the profiles
identified by a list of user_ids
```python
user_ids = [
    12770260,
    12769405
]
two_users = talent_api.get_users(user_ids)
for user in two_users:
    print(user['firstname'])
```

**get_user_matching_jobs(INT user_id)** - Get a list of Jobs that may
be suitable for the user profile identified by user_id
```python
user_id = 12770260
user_matching_jobs = talent_api.get_user_matching_jobs(user_id)
for job in user_matching_jobs:
    print(job['job']['job_title'] + " - Score: " + str(job['score']))
```

**get_user_stories(INT user_id)** - Get a list of Stories posted by the user
identified by user_id
```python
user_id = 10961800
user_stories = talent_api.get_user_stories(user_id)
for story in user_stories:
    print(story['title'])
```

**create_user(DICT user_data)** - Create a new User profile, returns the new
User object
```python
user_data = {
    'firstname':'Tim',
    'lastname':'Wallace',
    'email':'twallace@synaptic.net',
    'password':'secretpass',
    'zipcode':78704
}
new_user = talent_api.create_user(user_data)
print new_user['formatted_name']
```

**search_users(DICT search_params, INT page, INT results_per_page)** - Get a
list of Users from the database using SPHINX search
```python
search_params = {
    "commitment_levels":1
}
page = 1
results_per_page = 10
searched_users = talent_api.search_users(search_params, page, results_per_page)
for user in searched_users:
    print user['formatted_name']
```

**update_user(INT user_id, DICT update_data)** - Update an existing User
profile identified by user_id, returns an updated User object
```python
update_user_data = {
    'lastname':'Flynt'
}
updated_user = talent_api.update_user(12770414, update_user_data)
print updated_user['formatted_name']
```

### Circle Functions
**get_circle(INT circle_id)** - Get a single Circle object for the circle
identified by circle_id
```python
circle_id = 375
circle = talent_api.get_circle(circle_id)
print circle['circle_name']
```

**get_circles(LIST circle_ids)** - Get a list of Circle objects for circles
identified by a list of circle_ids
```python
circle_ids = [
    375,
    372
]
circles = talent_api.get_circles(circle_ids)
for circle in circles:
    print circle['circle_name']
```

**get_circle_jobs(INT circle_id, INT offset, INT limit)** - Get a list of Job
objects posted to the circle identified by circle_id
```python
circle_id = 375
circle_jobs = talent_api.get_circle_jobs(circle_id)
for job in circle_jobs:
    print job['job_title']
```

**get_cricle_members(INT circle_id)** - Get a list of User objects for members
of the circle identified by circle_id
```python
circle_id = 375
cricle_members = talent_api.get_cricle_members(circle_id)
for user in cricle_members:
    print user['formatted_name']
```

**create_circle(DICT circle_data)** - Create a new Circle, returns a Circle
object
```python
new_circle_data = {
    'circle_name':'Fantastically Great Circle'
}
new_circle = talent_api.create_circle(new_circle_data)
print new_circle['circle_name']
```

**post_circle_story(INT circle_id, DICT story_data)** - Post a new Story to
the Circle identified by circle_id, returns a Circle object
```python
circle_id = 375
circle_story_data = {
    'title':'Great Story',
    'story':'This story is great.'
}
circle_story = talent_api.post_circle_story(circle_id, circle_story_data)
print circle_story['title']
```

**update_circle(INT circle_id, DICT update_data)** - Update an existing Circle
identified by circle_id, returns a updated Circle object
```python
circle_id = 375
update_circle_data = {
    'circle_name':'Awesomely Fantastically Great Circle'
}
updated_circle = talent_api.update_circle(circle_id, update_circle_data)
print updated_circle['circle_name']
```

### Story Functions
**get_story(INT story_id)** - Get a single Story object for the story post
identified by story_id
```python
story_id = 196
story = talent_api.get_story(story_id)
print story['title']
```

**get_stories(LIST story_ids)** - Get multiple Story objects for story posts
identified by a list of story_ids
```python
story_ids = [
    196,
    197
]
stories = talent_api.get_stories(story_ids)
for story in stories:
    print story['title']
```

**post_story(DICT story_data)** - Post a new story to a Circle, returns the
Story object
```python
new_story_data = {
    'title':'Great Story posted to Stories Resource',
    'story':('This story was posted to the stories resource, rather than being
        posted through a circle'),
    'circle_id':375
}
new_story = talent_api.post_story(new_story_data)
print new_story['title']
```

**update_story(INT story_id, DICT story_data)** - Update an existing Story
identified by story_id, returns the updated Story object
```python
story_id = 240
updated_story_data = {
    'title':'Story posted to Stories'
}

updated_story = talent_api.update_story(248, updated_story_data)
print updated_story['title']
```

**update_stories(LIST story_ids, DICT story_data)** - Update a set of existing
Stories identified by a list of story_ids, returns a list of the updated
Story objects
```python
story_ids = [
    247,
    246
]
multiple_updated_stories = talent_api.update_stories(story_ids, updated_story_data)
for updated_story in multiple_updated_stories:
    print updated_story['title']
```
