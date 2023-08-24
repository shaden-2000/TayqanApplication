# Tayqan Application
### Project Idea
A mobile application utilizing artificial intelligence technology. The main idea behind the app is to allow users, specifically health care providers, to identifies any potential drug interactions and provides information about drugs that may conflicts. it done either by taking a picture or uploading a picture of the drug and the AI model can detect the drug Additionally, the app offers the following services:
1. Organizing drugs schedules for patients.
2. Sending reminders to health care providers to administer drugs.
3. Warning health care providers about any conflicting drugs.
### DEMO


https://github.com/shaden-2000/TayqanApplication/assets/100734021/2ed4dcbe-319a-4f35-a932-24539b8de52a



### Language
* Dart

### Framework
* Flutter
* Android studio

### Front-end
* taking a picture
1. code
2. interface
```

  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        backgroundColor: Colors.black,
        body: Stack(
          children: <Widget>[
            // Camera View
            CameraView(resultsCallback), // ui/camera view class // resultsCallbackClassification

            // Bounding boxes
            boundingBoxes2(results),

            Align(
              alignment: Alignment.bottomCenter,
              child: DraggableScrollableSheet(
                initialChildSize: 0.4,
                minChildSize: 0.1,
                maxChildSize: 0.5,
                builder: (_, ScrollController scrollController) => Container(
                  width: double.maxFinite,
                  decoration: BoxDecoration(
                      color: Colors.white.withOpacity(0.9),
                      borderRadius: BORDER_RADIUS_BOTTOM_SHEET),
                  child: SingleChildScrollView(
                    controller: scrollController,
                    child: Center(
                      child: Column(
                        mainAxisSize: MainAxisSize.min,
                        children: [
                          Icon(Icons.keyboard_arrow_up,
                              size: 48, color: Colors.orange),
                          (results != null) //  classification
                              ? Padding(
                            padding: const EdgeInsets.all(8.0),
                            child: Column(
                              children: [
                                StatsRow(
                                    'Drug Name:', '${results![0]!.className}'),

                                SizedBox(height: 8,),
                                ElevatedButton(
                                  style: ElevatedButton.styleFrom(
                                    backgroundColor: Color(0xffb2c7e5),
                                    shadowColor: Color(0xffFFC6D8),
                                    elevation: 5,
                                    shape: RoundedRectangleBorder(
                                   
                                        borderRadius: BorderRadius.circular(20.0)),
                                  ),
                                  onPressed: () {
                                    if (results != null) {
                                      //  print("GOT IN IF 1");
                                      if ("${results![0]!.className}" == "Peevo") {
                                        //  print("GOT IN IF IF 1");
                                        Navigator.push(context,
                                            MaterialPageRoute(builder: (context) => HomeScreen()));
                                      } else if ("${results![0]!.className}" == "Disprin 81") {
                                        //  print("GOT IN ELSE IF IF 2");
                                        Navigator.push(context,
                                            MaterialPageRoute(builder: (context) => HomeScreen1()));
                                      } else if ("${results![0]!.className}" == "Klavox") {
                                        //  print("GOT IN ELSE IF IF 2");
                                        Navigator.push(context,
                                            MaterialPageRoute(builder: (context) => HomeScreen2()));
                                      } else if ("${results![0]!.className}" == "Zinoximor") {
                                        //  print("GOT IN ELSE IF IF 2");
                                        Navigator.push(context,
                                            MaterialPageRoute(builder: (context) => HomeScreen3()));
                                      } else if ("${results![0]!.className}" == "Brufen") {
                                        //  print("GOT IN ELSE IF IF 2");
                                        Navigator.push(context,
                                            MaterialPageRoute(builder: (context) => HomeScreen4()));
                                      } else if ("${results![0]!.className}" == "Tabocine 100mg") {
                                        //  print("GOT IN ELSE IF IF 2");
                                        Navigator.push(context,
                                            MaterialPageRoute(builder: (context) => HomeScreen5()));
                                      }
                                      else if ("${results![0]!.className}" == "Vital E"||"${results![0]!.className}" == "Evit")
                                      {
                                        //  print("GOT IN ELSE IF IF 2");
                                        Navigator.push(context,
                                            MaterialPageRoute(builder: (context) => HomeScreen6()));
                                      }
                                  },
                                  child: const Text(
                                    'Show Interactions',
                                    style: TextStyle(
                                      fontSize: 15,
                                      letterSpacing: 0,
                                      fontFamily: 'DIN Next LT Arabic',
                                      fontWeight: FontWeight.bold,
                                      color: Color(0xFFFFFFFF),
                                    ),
                                    textAlign: TextAlign.center,
                                    softWrap: true,
                                  ),
                                ),
                              

                              ],
                            ),
                          )
                              : Container()

                        ],
                      ),
                    ),
                  ),
                ),
              ),
            )
          ],
        ),
      ),
    );
  }
```

![resize-16929082421801785349livecamera](https://github.com/shaden-2000/TayqanApplication/assets/100734021/ef3822ca-7f64-4783-ae1d-3d4f5645fed1)




* Upload a photo
```
 //run an image model
 Future runObjectDetectionWithoutLabels() async {
  //pick a random image
  final XFile? image = await _picker.pickImage(source: ImageSource.gallery);
  objDetect = await _objectModel
      .getImagePredictionList(await File(image!.path).readAsBytes());
  objDetect.forEach((element) {
   print({
    "score": element?.score,
    "className": element?.className,
    "class": element?.classIndex,
    "rect": {
     "left": element?.rect.left,
     "top": element?.rect.top,
     "width": element?.rect.width,
     "height": element?.rect.height,
     "right": element?.rect.right,
     "bottom": element?.rect.bottom,
    },
   });
  });
  setState(() {
   //this.objDetect = objDetect;
   _image = File(image.path);
  });
 }
```
* Model Integration

```
  //load your model
  Future loadModel() async {
    String pathImageModel = "assets/models/model_classification.pt";
    //String pathCustomModel = "assets/models/custom_model.ptl";
    String pathObjectDetectionModel = "assets/models/best.torchscript";
    try {
      _imageModel = await FlutterPytorch.loadClassificationModel(
          pathImageModel, 224, 224,
          labelPath: "assets/labels/label_classification_imageNet.txt");
      //_customModel = await PytorchLite.loadCustomModel(pathCustomModel);
      _objectModel = await FlutterPytorch.loadObjectDetectionModel(
          pathObjectDetectionModel, 9, 640, 640,
          labelPath: "assets/labels/labels.txt");
    } catch (e) {
      if (e is PlatformException) {
        print("only supported for android, Error is $e");
      } else {
        print("Error is $e");
      }
    }
  }
```

* show drug interactions
1. code
2. interface

```
              onPressed: () {
                if (objDetect != null) {
                  //  print("GOT IN IF 1");
                  if ("${objDetect![0]!.className}" == "Peevo") {
                    //  print("GOT IN IF IF 1");
                    Navigator.push(context,
                        MaterialPageRoute(builder: (context) => HomeScreen()));
                  } else if ("${objDetect![0]!.className}" == "Disprin 81") {
                    //  print("GOT IN ELSE IF IF 2");
                    Navigator.push(context,
                        MaterialPageRoute(builder: (context) => HomeScreen1()));
                  } else if ("${objDetect![0]!.className}" == "Klavox") {
                    //  print("GOT IN ELSE IF IF 2");
                    Navigator.push(context,
                        MaterialPageRoute(builder: (context) => HomeScreen2()));
                  } else if ("${objDetect![0]!.className}" == "Zinoximor") {
                    //  print("GOT IN ELSE IF IF 2");
                    Navigator.push(context,
                        MaterialPageRoute(builder: (context) => HomeScreen3()));
                  } else if ("${objDetect![0]!.className}" == "Brufen") {
                    //  print("GOT IN ELSE IF IF 2");
                    Navigator.push(context,
                        MaterialPageRoute(builder: (context) => HomeScreen4()));
                  } else if ("${objDetect![0]!.className}" == "Tabocine 100mg") {
                    //  print("GOT IN ELSE IF IF 2");
                    Navigator.push(context,
                        MaterialPageRoute(builder: (context) => HomeScreen5()));
                  }
                  else if ("${objDetect![0]!.className}" == "Vital E"||"${objDetect![0]!.className}" == "Evit")
                  {
                    //  print("GOT IN ELSE IF IF 2");
                    Navigator.push(context,
                        MaterialPageRoute(builder: (context) => HomeScreen6()));
                  }

                }
              }
```

<img width="152" alt="Screenshot 2023-07-26 053845" src="https://github.com/shaden-2000/TayqanApplication/assets/100734021/a0001f7a-3b42-42d6-810d-5248a5fc4292">

* drug interaction information
1. code
2. interface

```
Text(
              'Drug Interaction:',
              style: TextStyle(
                  fontFamily: 'DIN Next LT Arabic',
                  fontSize: 10,
                  color: Color.fromRGBO(223, 68, 100, 1),
                  fontWeight: FontWeight.w900),
              textAlign: TextAlign.center,
            ),
            // Text("تفاعل الدواء مع الدواء",style: TextStyle(fontFamily:'Roboto',fontSize: 10,color: Color.fromRGBO(223, 68, 100, 1),fontWeight: FontWeight.w900),textAlign: TextAlign.center,),//22
            Text(
              '--------------- ${drug.drug_interaction} & ${drug.drug_name} ---------------',
              style: TextStyle(
                fontFamily: 'DIN Next LT Arabic',
                fontSize: 8,
                color: Colors.black54,
                fontWeight: FontWeight.w900,
              ),
              textAlign: TextAlign.center,
            ),

            Padding(
              padding: const EdgeInsets.only(top: 30.0),
              child: Text(
                '${drug.description}',
                style: TextStyle(
                  fontFamily: 'DIN Next LT Arabic',
                  fontSize: 7,
                  color: Colors.black,
                  fontWeight: FontWeight.w800,
                ),
                textAlign: TextAlign.center,
                softWrap: true,
              ),
            ), //17

            Padding(
              padding: const EdgeInsets.all(20.0),
              child: Text(
                "Risk Level: ",
                style: TextStyle(
                    fontFamily: 'DIN Next LT Arabic',
                    fontSize: 10,
                    color: Color.fromRGBO(223, 68, 100, 1),
                    fontWeight: FontWeight.w900),
                textAlign: TextAlign.center,
              ),
            ),

            Container(
              child: drug.id == 1
                  ? _indecator1()
                  : drug.id == 2
                      ? _indecator2()
                      : drug.id == 3
                          ? _indecator3()
                          : Text("Loaded and No Error"),
            )
```
<img width="204" alt="Screenshot 2023-07-26 063526" src="https://github.com/shaden-2000/TayqanApplication/assets/100734021/3ad9b31e-b1f9-4118-8f68-3c9be781ef09">


### back-end
firebase is the database that been used , this is how to fetch the data image & name
```
  Future<void> getpeevo7Data() async {
    List<HomeModel> newList = [];
    QuerySnapshot peevo7SnapShot =
    await FirebaseFirestore.instance.collection("interaction7(Peevo)").get();
    peevo7SnapShot.docs.forEach(
          (element) {
            peevointeract7 = HomeModel(
                image: element["image"] ,BrandName: element["BrandName"]);
            newList.add(peevointeract7);
      },
    );
    peevo7 = newList;
    notifyListeners();
  }
```
