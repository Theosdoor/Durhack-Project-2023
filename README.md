# stupid-reliable-leech
Durhack repository for team: stupid-reliable-leech.

![Our father, Daniel Chambers](https://github.com/nqvm/stupid-reliable-leech/blob/8808a928c147140689c88224ec6f149ef17f02fa/Daniel-Chambers-Feature.png)

- [Durhack live](https://live.durhack.com/)  
- [Megateams](https://megateams.durhack.com/hacker)
- [Devpost](https://durhack-2023.devpost.com/)
- [MLH Prizes (not all of 'em)](https://hack.mlh.io/durhack-2023-4f/prizes)

## I Introduction  
CNN (goated.keros) model was developed on [this](https://www.kaggle.com/code/madz2000/cnn-using-keras-100-accuracy/notebook). This CNN model was trained on 50 x 50 pixel images, with greyscale values between 0-255.

## II How to use the website

## III How to use the CNN without the website
**Input:** Single 50 x 50 pixel image with greyscale values between 0-255.  
**Using the model:**  First, load the model:
```
import tensorflow as tf
model = tf.keras.models.load_model("filepath/to/goated.keras")
```   
This is further outlined on [this page](https://www.tensorflow.org/guide/keras/serialization_and_saving). To put in an input image, we must resize it in order to be accepted by the model. The code below shows how to take an input image, img.jpg:
```
image_path = 'path/to/img.jpg'
image_size = [50,50]

# Convert image to tensor
image = tf.io.read_file(image_path)
image = tf.io.decode_jpeg(image, channels = 1) # This greyscales the image as well
image = tf.image.resize(image, image_size)

# Convert to numpy array
data = image.numpy() / 255 # to normalise the data
pred = model.predict(data.reshape(-1, 50, 50, 1)) # reshape to be accepted by model
pred_arr = np.array(pred[0])

# Link to letter predictions, and print 3 most likely letters according to the model.

letterpred = ['A', 'B', 'C', 'D', 'E', 'F', 'G', 'H', 'I', 'J', 'K', 'L', 'M', 'N', 'O', 'P', 'Q', 'R', 'S', 'T', 'U', 'V', 'W', 'X', 'Y', 'Z', 'nothing']

letter_prediction_dict = {letterpred[i]: predarray[i] for i in range(len(letterpred))}
predarrayordered = sorted(predarray, reverse=True)
high1 = predarrayordered[0]
high2 = predarrayordered[1]
high3 = predarrayordered[2]
for key,value in letter_prediction_dict.items():
    if value==high1:
        print("Predicted Character 1: ", key)
        print('Confidence 1: ', 100*value)
    elif value==high2:
        print("Predicted Character 2: ", key)
        print('Confidence 2: ', 100*value)
    elif value==high3:
        print("Predicted Character 3: ", key)
        print('Confidence 3: ', 100*value)
```

### Important Links

- [Inspiration and starting point for CNN](https://www.kaggle.com/code/madz2000/cnn-using-keras-100-accuracy/notebook#Loading-the-ASL-dataset)
- [^ same](https://towardsdatascience.com/sign-language-recognition-with-advanced-computer-vision-7b74f20f3442)
- [First dataset used](https://www.kaggle.com/datasets/datamunge/sign-language-mnist)
- [Second (and larger) dataset](https://www.kaggle.com/datasets/grassknoted/asl-alphabet/data)
- [CNN Tutorial](https://www.kaggle.com/code/ryanholbrook/the-convolutional-classifier)
