# Content Based Routing

In this example you can deep dive into using a *Choice* router using Anypoint Studio to route messages in a flow.

This example application performs the following actions:

1. Listens for messages.
2. Passes messages to a *Set Variable* component that sets the variable `city` to the city that is passed in the message by the query parameter `city`.
3. Uses a  *Choice* router to find out whether each message contains a `city` attribute. The presence and value of this attribute determine how the *Choice* router routes the message:

  - If the value is `Sydney`, the router routes the message to a *Set Payload* component that is named *Popular City*. This latter component returns the message `NSW` to the requester.
  - If the value is `Adelaide`, the router routes the message to a *Set Payload* component that is named *State of Landmarks*. This latter component returns the message `SA` to the requester.
  - If the value is `Brisbane`, the router routes the message to a *Set Payload* component that is named *Sunshire State*. This latter component returns the message `QLD` to the requester.
  - If the message contains no `city` attribute, the router routes the message to the default path, which is a subflow that:

    1. Logs the message "No City has been specified, so using ACT as a default. " to the console
    1. Sets the value of `city` to `Canberra`.
    1. Returns the message `ACT`.

This example demonstrates that, when you are planning to route messages in a flow by using a *Choice* router, there are four aspects to planning that you need to consider:

* The content that the *Choice* router evaluates to determine how it routes messages
* The number of routes
* The default routing option
* The processing that the flow performs for each routing option

### Set Up and Run the Example

1. Import the Project content_based_routing_ using Anypoint Studio. 
2. Run the project by right-clicking its main folder and selecting **Run As > Mule Application**.
3. Open any web browser, paste the following URL in the address bar, and press Enter:

        http://localhost:8081/?city=Sydney

      **Result:** Your browser presents a message that reads "NSW".
   

4. In your browser (or using SOAPUI) address bar, replace the current URL with this one, and then press Enter:

        http://localhost:8081/?city=Brisbane

      **Result:** Your browser presents a message that reads "QLD". 
      
5. Try accessing `localhost:8081` without specifying a city: it should display "ACT"

        http://localhost:8081

 
