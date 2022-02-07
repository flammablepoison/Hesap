# Hesap
import 'package:flutter/material.dart';
import 'package:function_tree/function_tree.dart';

void main() => runApp(const MyApp());

class MyApp extends StatelessWidget {
  const MyApp({Key? key}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      debugShowCheckedModeBanner: false,
      title: 'Flutter Demo',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: const MyHomePage(),
    );
  }
}

class MyHomePage extends StatelessWidget {
  const MyHomePage({Key? key}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      endDrawer: Column(
        mainAxisAlignment: MainAxisAlignment.end,
        children: [
          //Bottom drawer
          SizedBox(
              height: MediaQuery.of(context).size.height * 0.7,
              width: MediaQuery.of(context).size.width * 0.6,
              child: Drawer(backgroundColor: Colors.blueGrey[800])),
        ],
      ),
      body: const Callocutor(),
    );
  }
}

class Callocutor extends StatefulWidget {
  const Callocutor({Key? key}) : super(key: key);

  @override
  _CallocutorState createState() => _CallocutorState();
}

class _CallocutorState extends State<Callocutor> {
  //İmportant data
  String toplama = '';
  String toplama1 = '';
  final numberContainerColor = Colors.black;
  final numberContainerColor2 = Colors.red[800];

  List numbers = [
    '7',
    '4',
    '1',
    ',',
    '8',
    '5',
    '2',
    '0',
    '9',
    '6',
    '3',
    '=',
    'SİL',
    '÷',
    'x',
    '-',
    '+'
  ];
// Clickable number box
  Widget number({@required number, @required color, @required onTap}) {
    return InkWell(
      onTap: onTap,
      child: Ink(
        //margin: EdgeInsets.only(top:5),
        color: color,
        width: MediaQuery.of(context).size.width * 0.235,
        height: MediaQuery.of(context).size.height * 0.175,
        child: Center(
          child: Text(
            number,
            style: const TextStyle(
              color: Colors.white,
              fontSize: 30,
            ),
          ),
        ),
      ),
    );
  }

  //Number box whole
  Widget numberSorting(
      {@required nl,
      @required nc,
      @required ot,
      @required nl2,
      @required nc2,
      @required ot2,
      @required nl3,
      @required nc3,
      @required ot3,
      @required nl4,
      @required nc4,
      @required ot4}) {
    return Column(
      children: [
        number(number: nl, color: nc, onTap: ot),
        number(number: nl2, color: nc2, onTap: ot2),
        number(number: nl3, color: nc3, onTap: ot3),
        number(number: nl4, color: nc4, onTap: ot4),
      ],
    );
  }

  Widget ifade({@required number, @required color, @required onTap, onLP}) {
    return InkWell(
      onTap: onTap,
      onLongPress: onLP,
      child: Ink(
        //margin: EdgeInsets.only(top:5),
        color: color,
        width: MediaQuery.of(context).size.width * 0.235,
        height: MediaQuery.of(context).size.height * 0.140,
        child: Center(
          child: Text(
            number,
            style: const TextStyle(
              color: Colors.white,
              fontSize: 30,
            ),
          ),
        ),
      ),
    );
  }

  Widget ifadeSorting(
      {@required nl,
      @required nc,
      @required ot,
      @required onlp,
      @required nl2,
      @required nc2,
      @required ot2,
      @required nl3,
      @required nc3,
      @required ot3,
      @required nl4,
      @required nc4,
      @required ot4,
      @required nl5,
      @required nc5,
      @required ot5}) {
    return Column(
      children: [
        ifade(number: nl, color: nc, onTap: ot, onLP: onlp),
        ifade(number: nl2, color: nc2, onTap: ot2),
        ifade(number: nl3, color: nc3, onTap: ot3),
        ifade(number: nl4, color: nc4, onTap: ot4),
        ifade(number: nl5, color: nc5, onTap: ot5),
      ],
    );
  }

//Bottom Drawer
  Widget drawerContainer() {
    return Container(
      color: Colors.blueGrey[800],
      width: MediaQuery.of(context).size.width * 0.06,
      height: MediaQuery.of(context).size.height * 0.7,
      child: InkWell(
          onTap: () {
            Scaffold.of(context).openEndDrawer();
          },
          child: const Icon(Icons.arrow_back_ios_new_outlined)),
    );
  }

  void lastIndex(sayiEkle) {    
if(toplama.length==0 && numbers[sayiEkle]=='-'){
        toplama = toplama + numbers[sayiEkle];
}else{
    switch (toplama[toplama.length - 1]) {
      case '+':
        break;
      case '-':
        break;
      case 'x':
        break;
      case '÷':
        break;
      case '=':
        break;
      case ',': 
        break;
      default:
        toplama = toplama + numbers[sayiEkle];
    }
  }}

  //İşlemlerin yapıldığı yer
  Widget islem() {
    return Column(
      crossAxisAlignment: CrossAxisAlignment.end,
      children: [
        SizedBox(
          width: MediaQuery.of(context).size.width * 1,
          height: MediaQuery.of(context).size.height * 0.08,
        ),
        SingleChildScrollView(
          padding: EdgeInsets.fromLTRB(5, 0, 5, 0),
          scrollDirection: Axis.horizontal,
          child: Text(
            '$toplama',
            style: TextStyle(
              fontSize: 40,
              color: Colors.black,
            ),
          ),
        )
      ],
    );
  }

  @override
  Widget build(BuildContext context) {
    return Column(
      children: [
        //transaction display
        Container(
          color: Colors.white,
          width: MediaQuery.of(context).size.width * 1,
          height: MediaQuery.of(context).size.height * 0.3,
          child: islem(),
        ),

        //Bottom Number and icon Container
        SizedBox(
          width: MediaQuery.of(context).size.width * 1,
          height: MediaQuery.of(context).size.height * 0.7,
          child: Row(
            mainAxisAlignment: MainAxisAlignment.start,
            children: [
              numberSorting(
                nl: numbers[0],
                nc: numberContainerColor,
                ot: () {
                  setState(() {
                    toplama = toplama + numbers[0];
                  });
                },
                nl2: numbers[1],
                nc2: numberContainerColor,
                ot2: () {
                  setState(() {
                    toplama = toplama + numbers[1];
                  });
                },
                nl3: numbers[2],
                nc3: numberContainerColor,
                ot3: () {
                  setState(() {
                    toplama = toplama + numbers[2];
                  });
                },
                nl4: numbers[3],
                nc4: numberContainerColor,
                ot4: () {
                  setState(() {
                    lastIndex(3);
                  });
                },
              ),
              numberSorting(
                nl: numbers[4],
                nc: numberContainerColor,
                ot: () {
                  setState(() {
                    toplama = toplama + numbers[4];
                  });
                },
                nl2: numbers[5],
                nc2: numberContainerColor,
                ot2: () {
                  setState(() {
                    toplama = toplama + numbers[5];
                  });
                },
                nl3: numbers[6],
                nc3: numberContainerColor,
                ot3: () {
                  setState(() {
                    toplama = toplama + numbers[6];
                  });
                },
                nl4: numbers[7],
                nc4: numberContainerColor,
                ot4: () {
                  setState(() {
                    toplama = toplama + numbers[7];
                  });
                },
              ),
              numberSorting(
                  nl: numbers[8],
                  nc: numberContainerColor,
                  ot: () {
                    setState(() {
                      toplama = toplama + numbers[8];
                    });
                  },
                  nl2: numbers[9],
                  nc2: numberContainerColor,
                  ot2: () {
                    setState(() {
                      toplama = toplama + numbers[9];
                    });
                  },
                  nl3: numbers[10],
                  nc3: numberContainerColor,
                  ot3: () {
                    setState(() {
                      toplama = toplama + numbers[10];
                    });
                  },
                  nl4: numbers[11],
                  nc4: numberContainerColor,
                  ot4: () {
                    setState(() {
                      String toplama1 = toplama
                          .replaceAll('x', '*')
                          .replaceAll(',', '.')
                          .replaceAll('÷', '/');
                      num metinSayisi = toplama1.interpret();
                      toplama1 = metinSayisi.toString();
                      toplama=toplama1.replaceAll('.', ',');
                    });
                  }),
              ifadeSorting(
                  nl: numbers[12],
                  nc: numberContainerColor2,
                  ot: () {
                    setState(() {
                      toplama = toplama.substring(0, toplama.length - 1);
                    });
                  },
                  onlp: () {
                    setState(() {
                      toplama = '';
                    });
                  },
                  nl2: numbers[13],
                  nc2: numberContainerColor2,
                  ot2: () {
                    setState(() {
                      lastIndex(13);
                    });
                  },
                  nl3: numbers[14],
                  nc3: numberContainerColor2,
                  ot3: () {
                    setState(() {
                      lastIndex(14);
                    });
                  },
                  nl4: numbers[15],
                  nc4: numberContainerColor2,
                  ot4: () {
                    setState(() {
                      lastIndex(15);
                    });
                  },
                  nl5: numbers[16],
                  nc5: numberContainerColor2,
                  ot5: () {
                    setState(() {
                      lastIndex(16);
                    });
                  }),
              SizedBox(
                child: drawerContainer(),
              )
            ],
          ),
        )
      ],
    );
  }
}
