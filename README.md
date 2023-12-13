# calories-cv-ml
Machine learning repository for calories-cv

## Objective
The objective of this repo is simply to document down all the steps required from data acquistion to data cleaning and processing all the way until model training. Here, we list down the main obstacles encountered and what the plan is.

### Data Acquistion
We first need to start with data acquisition. Unfortunately, after attempting to search for open source food dataset online, we are not able to find datasets suitable for our use case. As such, we have decided to instead create our own dataset.

### Dataset Creation
The idea is simple:
Create an interface that combs the web for food images based on the paramaters passed in. For example, we could pass in "chicken rice" to this interface and the interface will comb the web and automatically download images of chicken rice.  

That of course, leads us to question: how do we know that these images that we downloaded are indeed accurate representations? It is a valid concern. The plan, then, is to create another interface that allows us to easily dispose of images that inaccurately represents the queried food. This interface could also extend to create bounding boxes or other forms of label for easy data processing. There are already existing tools for this, such as label studio, but I would like to explore creating such an interface by myself.

The interface I created can be found at: https://github.com/jonechong/image-labeller

#### Data Labelling (done with image-labeller linked above)
For the images to be useful in training a machine learning model, they need to be labeled accurately. This involves:

*Verifying each image to ensure it accurately represents the queried food item.
*Annotating images with relevant information such as food type, ingredients, and possibly estimated calorie content.

#### Image Processing
Once the images are downloaded, they need to be processed to ensure uniformity and quality. This includes:

*Resizing images to a standard dimension for consistency.
*Normalizing pixel values for better model performance.
*Augmenting the training dataset with transformations (like rotations, flips, etc.) to increase its robustness.
We do augmentation also because our dataset size is not huge (only ~200 per food category as per the time of this writing), so we want the model to have some variety so that it generalises well.

### Model Training
#### Model Selection
Given the nature of the task (image classification), a convolutional neural network (CNN) is suitable. Specifically, we are using MobileNetV2 due to its efficiency in handling image data with a relatively lower computational cost.

Training Process
*Preprocessing: Images are preprocessed as per the dataset creation steps.
*Splitting Data: The dataset is divided into training, validation, and test sets.
*Model Architecture: Modifications are made to MobileNetV2 to suit our specific needs, such as adjusting the output layer to match the number of food categories.
*Training: The model is trained using the training set, with validation performed at intervals to monitor performance and avoid overfitting.
*Hyperparameter Tuning: Parameters such as learning rate, batch size, and number of epochs are adjusted to optimize performance.

#### Evaluation
The model's performance is evaluated using the test set. Metrics such as accuracy are considered to assess the model's ability to classify images correctly.

#### Model Deployment
The trained model is exported for deployment, in ONNX format for compatibility and efficiency in inference tasks. This model is then integrated with the backend (refer to backend repo: https://github.com/jonechong/calories-cv-backend/tree/d4fb955a1e180af30dea5a6256ba92d2e5755cac) (using FastAPI) to create an endpoint that receives image data and returns predictions.


Parent repo: https://github.com/jonechong/calories-cv
