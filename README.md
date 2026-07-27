# fwd-vision-ai-kit

Vision AI Kit, by Forward Education.

Find us at [forwardedu.com](https://forwardedu.com/) and [learn.forwardedu.com](https://learn.forwardedu.com/). Learn more about the Vision AI Kit on the [product page](https://forwardedu.com/products/vision-ai-kit-exploration).

### ~ reminder

![works with micro:bit V2 only image](/static/v2/v2-only.png)

These blocks require the [micro:bit V2](/device/v2). If you use them with a V1 micro:bit you will see the 927 error code on the screen.

### ~

## Example Usage

Our learning systems are designed to simplify teaching coding and computer science for educators at all experience levels. Our Vision AI Kit can be used on its own or joined with other kits to access our wider library of sensors, motors, lights, and buttons. Check out our libraries of [lessons](https://learn.forwardedu.com/lesson-library), [projects](https://learn.forwardedu.com/projects/), and [tutorials](https://learn.forwardedu.com/tutorials/). Samples of coding with the AI Vision Kit can be seen below.

Train the micro:bit to recognize friendly faces. First the module is initialized and set to Face Recognition mode. Then, when you see the camera pick up a friendly face press A to give it the ID of 1. You can give the ID to more than 1 face. On every iteration of the forever loop the program will take note of what's on the screen. If a friendly face (ID 1) is detected on the screen then the micro:bit shows a smiley. If there are no friendly faces then it shows a sad face. We can reset the training by pressing B.

```blocks
input.onButtonPressed(Button.A, function () {
    fwdAiVision.writeLearn1(1)
})
input.onButtonPressed(Button.B, function () {
    fwdAiVision.forgetLearn()
})
fwdAiVision.initI2c()
fwdAiVision.initMode(fwdAiVision.protocolAlgorithm.ALGORITHM_FACE_RECOGNITION)
basic.forever(function () {
    fwdAiVision.request()
    if (fwdAiVision.isAppear(1, HUSKYLENSResultType_t.HUSKYLENSResultBlock)) {
        basic.showIcon(IconNames.Happy)
    } else {
        basic.showIcon(IconNames.Sad)
    }
})
```

Train the micro:bit to recognize different faces. We have some of the same elements as before: initialization, set to Face Recognition mode, A to learn, get data from screen forever, B to forget. Now we've initialized a variable faceID to 1, and every time we learn a face we add 1 to faceID and when we forget training data we reset faceID to 1. The logic in the forever loop has been changed. We check if a face is detected on screen. If there is we show the ID that corresponds to the face. Unrecognized faces show up as ID 0.

```blocks
input.onButtonPressed(Button.A, function () {
    fwdAiVision.writeLearn1(faceID)
    faceID += 1
})
input.onButtonPressed(Button.B, function () {
    fwdAiVision.forgetLearn()
    faceID = 1
})
let faceID = 0
fwdAiVision.initI2c()
fwdAiVision.initMode(fwdAiVision.protocolAlgorithm.ALGORITHM_FACE_RECOGNITION)
faceID = 1
basic.forever(function () {
    fwdAiVision.request()
    if (fwdAiVision.isAppear_s(HUSKYLENSResultType_t.HUSKYLENSResultBlock)) {
        basic.showNumber(fwdAiVision.readBox_s(Content3.ID))
    } else {
        basic.clearScreen()
    }
})
```

## Supported Targets

- for PXT/microbit

## License

MIT
