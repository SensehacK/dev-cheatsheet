# Setup

## Enum
First setup [viewState](viewState.md) enum which will conform to bunch of protocols. But this is our construct / gateway to interacting application state at the given point of time with particular screen or module implementation.

## Protocols

Of course the compiler will shout at you saying can't find these protocols and what not.
So we need to create another file to make these protocols accessible. Of course I'm gonna leave the `access modifier` to your preference how your project is structured.

Utilize [viewStateProtocol](viewStateProtocol.md) code to define our protocols and their internal protocol dependencies.

## Extensions

Before we start bridging the viewstate types we need to provide some extensions to the protocol we added.
You can add those by following this file [viewStateExtensions](viewStateExtensions.md)

## Bridging 

In order to quickly bridge states utilizing `Driver` or `ObservableType` in RxSwift. 
We can quickly jump over to this file to create bridging helper methods.
[viewStateBridgeVCVM](viewStateBridgeVCVM.md) 

## Empty States

Now you would want to have these empty states copied over when you're interacting with ViewStateProtocol and need to provide one of those four protocol bounded states.
This gives us the flexibility of having options to give the reader that we are planning to implement that customState in future but for now just return { } 

## Input Output

Setup `Input and Output` as the foundation for interacting with ViewModel layer.
You need to create appropriate protocols around Input Output requirements.
Please follow this file [input_output](input_output.md)  in order to create respective protocols.

## ViewModel

Need to initialize the ViewModel with conformance to `ViewModellable` and another protocol to define `Input & Output` of that ViewModel.

Use this example to appropriately create ViewModel class to conform with this protocol types.
[viewStateViewModel](viewStateViewModel.md)

## View Controller

Use this file to create ViewController setup code.
[viewStateViewController](viewStateViewController.md)
This would be our last file to setup. Which ties in together how everything links with each other.

## Custom States

Of course having custom states associated with your custom data which can be passed back and forth around the different ViewStates an app is currently on gives us the flexibility to work around those states. 

You can find these custom states example in  [viewStateCustomModel](viewStateCustomModel.md)

And Voila now you're ready to do interaction between each other.

