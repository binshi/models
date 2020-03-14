Training neural networks focuses a lot on accuracy, such as detecting the right bounding boxes and having them placed in the right spot. But what should you actually do with bounding boxes, semantic masks, classes, etc.? How would a self-driving car make a decision about where to drive based solely off the semantic classes in an image?

It’s important to get useful information from your model - information from one model could even be further used in an additional model, such as traffic data from one set of days being used to predict traffic on another set of days, such as near to a sporting event.

For the traffic example, you’d likely want to count how many bounding boxes there are, but also make sure to only count once for each vehicle until it leaves the screen. You could also consider which part of the screen they come from, and which part they exit from. Does the left turn arrow need to last longer near to a big event, as all the cars seem to be heading in that direction?

In an earlier exercise, you played around a bit with the confidence threshold of bounding box detections. That’s another way to extract useful statistics - are you making sure to throw out low confidence predictions?

### MQTT {#mqtt}

MQTT stands for MQ Telemetry Transport, where the MQ came from an old IBM product line called IBM MQ for Message Queues \(although MQTT itself does not use queues\). That doesn’t really give many hints about its use.

MQTT is a lightweight publish/subscribe architecture that is designed for resource-constrained devices and low-bandwidth setups. It is used a lot for Internet of Things devices, or other machine-to-machine communication, and has been around since 1999. Port 1883 is reserved for use with MQTT.

### Publish/Subscribe {#publish-subscribe}

In the publish/subscribe architecture, there is a broker, or hub, that receives messages published to it by different clients. The broker then routes the messages to any clients subscribing to those particular messages.

This is managed through the use of what are called “topics”. One client publishes to a topic, while another client subscribes to the topic. The broker handles passing the message from the publishing client on that topic to any subscribers. These clients therefore don’t need to know anything about each other, just the topic they want to publish or subscribe to.

MQTT is one example of this type of architecture, and is very lightweight. While you could publish information such as the count of bounding boxes over MQTT, you cannot publish a video frame using it. Publish/subscribe is also used with self-driving cars, such as with the Robot Operating System, or ROS for short. There, a stop light classifier may publish on one topic, with an intermediate system that determines when to brake subscribing to that topic, and then that system could publish to another topic that the actual brake system itself subscribes to.

### Further Research {#further-research}

* Visit the [main site](http://mqtt.org/) for MQTT
* A [helpful post](https://internetofthingsagenda.techtarget.com/definition/MQTT-MQ-Telemetry-Transport) on more of the basics of MQTT

There is a useful Python library for working with MQTT called`paho-mqtt`. Within, there is a sub-library called`client`, which is how you create an MQTT client that can publish or subscribe to the broker.

To do so, you’ll need to know the IP address of the broker, as well as the port for it. With those, you can connect the client, and then begin to either publish or subscribe to topics.

Publishing involves feeding in the topic name, as well as a dictionary containing a message that is dumped to JSON. Subscribing just involves feeding in the topic name to be subscribed to.

You’ll need the[documentation](https://pypi.org/project/paho-mqtt/)for`paho-mqtt`to answer the quiz below.

### Further Research {#further-research}

* As usual, documentation is your friend. Make sure to check out the [documentation on PyPi](https://pypi.org/project/paho-mqtt/) related to the `paho-mqtt`
  Python library if you want to learn more about its functionality.
* Intel® has a [pretty neat IoT tutorial](https://software.intel.com/en-us/SetupGateway-MQTT) on working with MQTT with Python you can check out as well.

Sometimes, you may still want a video feed to be streamed to a server. A security camera that detects a person where they shouldn’t be and sends an alert is useful, but you likely want to then view the footage. Since MQTT can’t handle images, we have to look elsewhere.

At the start of the course, we noted that network communications can be expensive in cost, bandwidth and power consumption. Video streaming consumes a ton of network resources, as it requires a lot of data to be sent over the network, clogging everything up. Even with high-speed internet, multiple users streaming video can cause things to slow down. As such, it’s important to first consider whether you even need to stream video to a server, or at least only stream it in certain situations, such as when your edge AI algorithm has detected a particular event.

### FFmpeg {#ffmpeg}

Of course, there are certainly situations where streaming video is necessary. The[FFmpeg library](https://www.ffmpeg.org/)is one way to do this. The name comes from “fast forward” MPEG, meaning it’s supposed to be a fast way of handling the MPEG video standard \(among others\).

In our case, we’ll use the`ffserver`feature of FFmpeg, which, similar to MQTT, will actually have an intermediate FFmpeg server that video frames are sent to. The final Node server that displays a webpage will actually get the video from that FFmpeg server.

There are other ways to handle streaming video as well. In Python, you can also use a flask server to do some similar things, although we’ll focus on FFmpeg here.

### Setting up FFmpeg {#setting-up-ffmpeg}

You can download FFmpeg from ffmpeg.org. Using`ffserver`in particular requires a configuration file that we will provide for you. This config file sets the port and IP address of the server, as well as settings like the ports to receive video from, and the framerate of the video. These settings can also allow it to listen to the system stdout buffer, which is how you can send video frames to it in Python.

### Sending frames to FFmpeg {#sending-frames-to-ffmpeg}

With the`sys`Python library, can use`sys.stdout.buffer.write(frame)`and`sys.stdout.flush()`to send the frame to the`ffserver`when it is running.

If you have a`ffmpeg`folder containing the configuration file for the server, you can launch the`ffserver`with the following from the command line:

```
sudo ffserver 
-f
 ./ffmpeg/server.conf
```

From there, you need to actually pipe the information from the Python script to FFmpeg. To do so, you add the`|`symbol after the python script \(as well as being after any related arguments to that script, such as the model file or CPU extension\), followed by`ffmpeg`and any of its related arguments.

For example:

```
python app.py -m “model.xml” | ffmpeg -framerate 24
```

And so on with additional arguments before or after the pipe symbol depending on whether they are for the Python application or for FFmpeg.



[Node.js](https://nodejs.org/en/about/) is an open-source environment for servers, where Javascript can be run outside of a browser. Consider a social media page, for instance - that page is going to contain different content for each different user, based on their social network. Node allows for Javascript to run outside of the browser to gather the various relevant posts for each given user, and then send those posts to the browser.

In our case, a Node server can be used to handle the data coming in from the MQTT and FFmpeg servers, and then actually render that content for a web page user interface.

