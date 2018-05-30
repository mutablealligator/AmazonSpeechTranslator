# Speech Recognition, Translation, and Text-to-Speech on iOS
![License](https://img.shields.io/badge/Smiles-YES-red.svg) ![License](https://img.shields.io/dub/l/vibe-d.svg)

This is a powerful, yet simple solution for demonstrating the power of machine learning on mobile using managed cloud services. The app provides speech recognition via Apple Speech API, text translation via Amazon Translate, and showcases speech synthesis using Amazon Polly to read back our translated text!

|[Speech Recognition]()|[Translation]()|
|:--:|:--:| 
[![Recognition](https://s3-us-west-2.amazonaws.com/mobilequickie/speechtranslator/recognition-full.png)](https://s3-us-west-2.amazonaws.com/mobilequickie/speechtranslator/recognition-full.png)| [![Translation](https://s3-us-west-2.amazonaws.com/mobilequickie/speechtranslator/translation-full.png)](https://s3-us-west-2.amazonaws.com/mobilequickie/speechtranslator/translation-full.png) | 

## Getting Started
Of all the AWS services, Amazon Translate is by far the easiest to implement into your app. Amazon Polly is a close 2nd. So, if you have never used AWS before and want to try adding some machine learning to your mobile app, now is the time!

![Architectural Diagram](https://s3-us-west-2.amazonaws.com/mobilequickie/speechtranslator/speech-polly-diagram-noLambda.png "Speech Translator Architecture")

There are two easy steps to building this solution: 1. **Configure backend** by creating an Amazon Cognito Identity Pool, IAM Role(s), and adding permission to those roles for accessing Amazon Translate and Polly directly from a mobile app. 2. **Create a mobile app** to showcase natural language processing by cloning my sample app from GitHub and configuring it to use the values created in step #1.

## STEP 1: Configure Backend
I created a CloudFormation Stack to automate the creation of the Cognito Identity Pool, IAM Roles, and permissions so we can start playing with the app! The other services do not require any backend configuration and will be called directly from our mobile app.

1.	Click on the Launch Stack button
    
    [![Launch Stack](https://s3-us-west-2.amazonaws.com/mobilequickie/speechtranslator/launch-stack.svg)](https://console.aws.amazon.com/cloudformation/home?region=us-west-2#/stacks/new?stackName=speechtranslator-stack&templateURL=https://s3-us-west-2.amazonaws.com/mobilequickie/speechtranslator/SpeechTranslator-CloudFormation-Cognito.yaml)

    This will launch the AWS CloudFormation Console and automate the creation of a Cognitio Identity Pool, associated authenticate & authenticated IAM Roles along with policies for accessing Amazon Translate and Amazon Polly directly from a mobile app.
2.	Click **Next** on the Select Template page
3.	Click **Next**
4.	On the Options page, leave all the defaults and click **Next**
5.	On the Review page, check the box to acknowledge that CloudFormation will create IAM resources and click **Create**.
6.	Wait for the *speechtranslator-stack* stack to reach a status of CREATE_COMPLETE
7.	With the speechtranslator-stack selected, **click on the Outputs tab** and you should see three rows.
 ![Stack Output](https://s3-us-west-2.amazonaws.com/mobilequickie/speechtranslator/stack-output-final.png "CloudFormation Stack Output of Cognito Identity Pool details")
8.	Copy the Value for each of the three resources as we’ll be pasting those values into our service config in the AppDelegate of our mobile app.

## STEP 2: Mobile Client Setup
1. Download or clone this project
    ```
    $ git clone https://github.com/mobilequickie/AmazonSpeechTranslator.git

    $ cd AmazonSpeechTranslator
    ```
2. Install Cocoapods
    ```
    $ sudo gem install cocoapods

    $ pod install --repo-update
    ``` 
3. Launch project in Xcode
    ```
    $ open SpeechRec.xcworkspace
    ``` 
4. Update the AppDelegate.swift by pasting in your own identityPoolId, unauthRoleArn, and authRoleArn from the output tab of CloudFormation Stck that you created in Step #1
 ![Stack Output](https://s3-us-west-2.amazonaws.com/mobilequickie/speechtranslator/appdelegate-stack-config.png "CloudFormation Stack Output of Cognito Identity Pool details")

5. Build and run the app 

## Requirements
- [Cocoapods](https://github.com/CocoaPods/CocoaPods) 1.2.0 +
- iOS 10.2+ / Mac OS X 10.13+
- Xcode 9.0+

## Built Using
* See THIRD-PARTY-LICENSES.txt
* [Pulsator](https://github.com/shu223/Pulsator) - Used for animating the live listener
* [DropDown](https://github.com/AssistoLab/DropDown) - Used as a dropdown for selecting the different languages

## Author

**Dennis Hills (Mobile Quickie)** - *Initial work*

[YouTube](https://www.youtube.com/channel/UC17JFcOf9l_DRQ3_NsV-V2g) |
[Blog](https://medium.com/@dmennis) |
[Twitter](https://twitter.com/dmennis)

## License

[![License](https://img.shields.io/dub/l/vibe-d.svg)](http://doge.mit-license.org)
This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details