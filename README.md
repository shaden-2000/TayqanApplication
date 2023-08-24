# Tayqan Application
### Project Idea
A mobile application utilizing artificial intelligence technology. The main idea behind the app is to allow users, specifically health care providers, to identifies any potential drug interactions and provides information about drugs that may conflicts. it done either by taking a picture or uploading a picture of the drug and the AI model can detect the drug Additionally, the app offers the following services:
1. Organizing drugs schedules for patients.
2. Sending reminders to health care providers to administer drugs.
3. Warning health care providers about any conflicting drugs.


### Language
* Dart

### Framework
* Flutter
* Android studio

### Front-end
* taking a picture
1. code
2. interface

>   Widget build(BuildContext context) {
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
