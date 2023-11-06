# calories-cv-ml
Machine learning repository for calories-cv

## Objective
The objective of this repo is simply to document down all the steps required from data acquistion to data cleaning and processing all the way until model training. Here, we list down the main obstacles encountered and what the plan is.
We first need to start with data acquisition. Unfortunately, after attempting to search for open source food dataset online, we are not able to find datasets suitable for our use case. As such, we have decided to instead create our own dataset.

### Dataset Creation
The idea is simple:
Create an interface that combs the web for food images based on the paramaters passed in. For example, we could pass in "chicken rice" to this interface and the interface will comb the web and automatically download images of chicken rice. That of course, leads us to question: how do we know that these images that we downloaded are indeed accurate representations? It is a valid concern. The plan, then, is to create another interface that allows us to easily dispose of images that inaccurately represents the queried food. This interface could also extend to create bounding boxes or other forms of label for easy data processing. 
