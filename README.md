# Kin Unity SDK tutorial
This is a simple implementation of  [Kin SDK for Unity](https://github.com/kinecosystem/kin-sdk-unity). It can work as a standalone implementation, or together with the server side implementation provided in the [Kin Unity SDK tutorial-server](https://github.com/hitwill/kin-sdk-unity-tutorial-server-python).


Within 5-10 minutes, you should be able to make and receive calls to [Kin's blockchain](https://www.kin.org/blockchainExplorer) from an Android client on Unity.

You can also extend it to suit your needs.


![Kin Unity implementation](https://i.imgur.com/6NWnk6D.png)



### Note
The main objective of this code is to get you interacting with the blockhain as quickly as possible, and to also understand a sample implementation. As such, abstraction is avoided and a wrapper is provided in a single file.


### Additional info
You can find detailed explanation of this code on [Stackoverflow](https://stackoverflow.com/questions/56096526/how-to-set-up-and-use-the-kin-blockchain-in-a-unity-app-step-by-step/56096527#56096527)



## Installation

1. Clone to your localhost directory
2. Open in Unity
3. Compile and run on an Android device or emulator.

## Requirements
[Kin Unity SDK](https://assetstore.unity.com/packages/tools/utilities/kin-sdk-for-unity-137182)

## Usage

You can immediately start usage with the tutorial app provided.

#### For your own project
1. Create an empty KinWrapper object in your scene, and attach the script: [Scripts/KinWrapper.cs ](https://github.com/hitwill/kin-sdk-unity-tutorial/blob/master/Assets/Scripts/KinWrapper.cs)
2. Place this object in any scene you wish to use the blockchain transactions

The object will initialize itself, maintain itself across scenes, and also listen to changes in the blockchain (e.g. payments/ balance changes).

#### Listening to Kin's blockchain
```csharp
    void Start()
    {
        string url = "https://mykin-server.com";
        string serverAddress = "GAFWSBEOGCCYVEC5YZUILDEDGHO27PODVTQJ45DSFBODKRXQ42MVLIZZ";
        kinWrapper = GameObject.Find("KinWrapper").GetComponent<KinWrapper>();
        kinWrapper.Initialize(ListenKin, url, serverAddress);
    }
    
```
#### Getting the balance
```csharp
    kinWrapper.Balance()
```

#### Sending a payment
```csharp
    kinWrapper.SendPayment(1.00M, "test send", address); 
```

You can find more examples in [Scripts/Tutorial.cs](https://github.com/hitwill/kin-sdk-unity-tutorial/blob/master/Assets/Scripts/Tutorial.cs)


The wrapper is pre-configured to use a test server, but you can modify the following variables to suit your needs:
```csharp
    private readonly string serverKinAddress = "GCMVZ4B6P4QEZL727UH2A6ABA2AYY67GZC3NILDD2DVSZPRN4QQCRATG"; //Kin address for your server TODO:/ enter server address here
    private readonly string appId = "1acd"; //appId assigned by Kin foundation. Use "1acd" for testing
    private readonly Kin.Environment environment = Kin.Environment.Test;
    //URL to your server
    private readonly string baseURL = "https://kin-sdk-unity-tutorial-server.herokuapp.com";
    //Your server URL  for client to request whitelisting
    private readonly string whitelistURL = "?whitelist=1";
    //Your server URL for client to request payments (from your server)
    private readonly string requestPaymentURL = "?request=1";
    //Your server URL for client to request payments (from your server)
    private readonly string fundURL = "?fund=1";
    private readonly float secondsBetweenRetry = 4f;
    private readonly int maxInitializes = 15; //times to try initializing in case of network error
    private readonly bool verbose = true; // upate caller on statuses of initialization 
```


## Contributing

Please read [CONTRIBUTING.md](https://gist.github.com/PurpleBooth/b24679402957c63ec426) for details.



## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details

