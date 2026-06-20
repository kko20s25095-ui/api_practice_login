import 'dart:convert';

import 'package:flutter/material.dart';
import 'package:http/http.dart' as http;
import 'package:snackbar/snackbar.dart';
import 'package:vlog/api/main_screen.dart';

class ApiExample extends StatefulWidget {
  const ApiExample({super.key});

  @override
  State<ApiExample> createState() => _ApiExampleState();
}

class _ApiExampleState extends State<ApiExample> {

  //테스트할 때 일일히 쓰기 귀찮아서 여기 기록해둠
  //"email": "user000@mod.com",
  //"password": "password123"

  //텍스트 필드 기본 준비 요소들
  TextEditingController _emailCtrl = TextEditingController();
  TextEditingController _passwordCtrl = TextEditingController();


  //토큰을 저장할 변수
  late String token;

  //나중에 상태코드 받아서 로그인처리할지 하는 함수 작성하면 될 듯

  Future<void> _tryLogin() async {
    final String baseUrl = "https://tank2401.dothome.co.kr";
    String url = "$baseUrl/auth/login";

    final response = await http.post(
        Uri.parse(url),
        headers: {
          "Content-Type": "application/json"
        },

        body: jsonEncode({
          "email": "${_emailCtrl.text}",
          "password": "${_passwordCtrl.text}"
        })
    );

    final data = jsonDecode(response.body);

    if(response.statusCode == 200){ //로그인 성공일 경우
      token = data['data']['token']; //여기서 전에 선언해둔 토큰을 받아올 것임
      print("로그인 성공 : 상태코드 ${response.statusCode}");
      ScaffoldMessenger.of(context).clearSnackBars();
      ScaffoldMessenger.of(context).showSnackBar(
          SnackBar(
            content: Text("로그인 성공"),
          )
      );
      Navigator.push(context, MaterialPageRoute(builder: (context) => MainScreen(),));
    }
    else if(response.statusCode == 401){
      print("아이디 또는 비밀번호가 일치하지 않음");
      ScaffoldMessenger.of(context).clearSnackBars();
      ScaffoldMessenger.of(context).showSnackBar(
          SnackBar(
            content: Text("로그인 실패"),
          )
      );
    }
    else {
      ScaffoldMessenger.of(context).clearSnackBars();
      ScaffoldMessenger.of(context).showSnackBar(
          SnackBar(
            content: Text("기타 에러 발생 : ${response.statusCode}"),
          )
      );
    }
  }




  @override
  Widget build(BuildContext context) {
    return Scaffold(
      backgroundColor: Color(0xFF5B2FD2), //배경 화면 색

      body: SafeArea(

        child: Column(
          children: [
            //최상단 Connex Chat 부분
            Row(
              children: [
                Padding(
                  padding: EdgeInsets.all(15),

                  child: Image.asset(
                      "assets/images/simbol-white.png"
                  ),
                ),

                Text(
                  "Connex Chat",
                  style: TextStyle(
                      fontSize: 25,
                      fontWeight: FontWeight.bold,
                      color: Colors.white
                  ),
                )
              ],
            ),

            //"안녕하세요!" 등 문구 부분

            SizedBox(height: 25,),

            Align(
              alignment: Alignment.topLeft,

              child: Padding(
                padding: EdgeInsets.only(left: 20, bottom: 3),

                child: Text(
                  "안녕하세요!",
                  style: TextStyle(
                      fontSize: 30,
                      fontWeight: FontWeight.bold,
                      color: Colors.white
                  ),
                ),
              ),
            ),

            Align(
              alignment: Alignment.topCenter,

              child: Padding(
                padding: EdgeInsets.only(left: 5),

                child: Text(
                  "Connex Chat과 함께 오늘도 활기찬 하루되세요",
                  style: TextStyle(
                      fontSize: 18,
                      fontWeight: FontWeight.bold,
                      color: Colors.white.withOpacity(0.7)
                  ),
                ),
              ),
            ),


            SizedBox(height: 40,),

            //로그인 텍스트 필드와 버튼이 존재하는 컨테이너
            Expanded(
              child: Container(
                  height: double.infinity,
                  width: double.infinity,

                  decoration: BoxDecoration(
                      borderRadius: BorderRadius.only(topLeft: Radius.circular(20), topRight: Radius.circular(20)),
                      color: Colors.white
                  ),

                  child: Padding(

                    padding: EdgeInsets.symmetric(horizontal: 24, vertical: 20),
                    child: SingleChildScrollView( //입력 키보드 등장 시 오버플로우를 해결하기 위해서 추가했음
                      child: Column(
                        crossAxisAlignment: CrossAxisAlignment.start,

                        children: [

                          Padding(
                            padding: const EdgeInsets.all(9.0),
                            child: Text(
                              "Login",
                              style: TextStyle(
                                  fontSize: 30,
                                  fontWeight: FontWeight.bold,
                                  color: Color(0xFF4B24D6)
                              ),
                            ),
                          ),

                          //텍스트 필드 부분 시작

                          // (1) 이메일 입력란
                          Padding(
                            padding: const EdgeInsets.symmetric(vertical: 8),
                            child: TextField(
                              controller: _emailCtrl,
                              onSubmitted: (value) {
                                //나중에 해야할 것
                              },

                              decoration:
                              InputDecoration(
                                  hintText: "이메일을 입력해주세요.",
                                  border: OutlineInputBorder(
                                      borderRadius: BorderRadius.circular(10)
                                  )
                              ),
                            ),
                          ),

                          //(2) 비밀번호 입력창
                          Padding(
                            padding: const EdgeInsets.symmetric(vertical: 8),
                            child: TextField(
                              controller: _passwordCtrl,
                              onSubmitted: (value) {
                                //나중에 해야할 것
                              },

                              decoration:
                              InputDecoration(
                                  hintText: "비밀번호를 입력해주세요.",
                                  border: OutlineInputBorder(
                                      borderRadius: BorderRadius.circular(10)
                                  )
                              ),
                            ),
                          ),

                          SizedBox(height: 170,),

                          // (3) 로그인 하기 버튼
                          GestureDetector(
                            onTap: () => _tryLogin(),

                            child: Container(
                              width: double.infinity,

                              decoration: BoxDecoration(
                                  color: Colors.white,
                                  borderRadius: BorderRadius.circular(10),
                                  border: Border.all(
                                    color: Color(0xFF5B2FD2),
                                  )
                              ),

                              child: Padding(
                                padding: const EdgeInsets.all(15),
                                child: Align(
                                  alignment: Alignment.center,

                                  child: Text(
                                    "로그인 하기",
                                    style: TextStyle(
                                        fontSize: 15,
                                        fontWeight: FontWeight.bold,
                                        color: Color(0xFF5B2FD2)
                                    ),
                                  ),
                                ),
                              ),
                            ),
                          ),

                          SizedBox(height: 20,),

                          // (4) 회원가입 버튼
                          GestureDetector(
                            onTap: () {
                              //나중에 해야할 것
                            },

                            child: Container(
                              width: double.infinity,

                              decoration: BoxDecoration(
                                  color: Color(0xFF5B2FD2),
                                  borderRadius: BorderRadius.circular(10),
                                  border: Border.all(
                                    color: Color(0xFF5B2FD2),
                                  )
                              ),

                              child: Padding(
                                padding: const EdgeInsets.all(15),
                                child: Align(
                                  alignment: Alignment.center,

                                  child: Text(
                                    "회원가입 하러가기",
                                    style: TextStyle(
                                        fontSize: 15,
                                        fontWeight: FontWeight.bold,
                                        color: Colors.white
                                    ),
                                  ),
                                ),
                              ),
                            ),
                          ),
                        ],
                      ),
                    ),
                  )
              ),
            )
          ],
        ),
      ),
    );
  }
}
