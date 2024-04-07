#include <Joystick.h>

// 定義 Joystick 物件
Joystick_ Joystick(JOYSTICK_DEFAULT_REPORT_ID, JOYSTICK_TYPE_GAMEPAD,
                   4, 0,                  // 按鈕數量，搖桿開關數量
                   true, true, false,     // X 和 Y，但沒有 Z 軸
                   false, false, false,   // 沒有 Rx、Ry 或 Rz
                   false, false,          // 沒有舵機或油門
                   false, false, false); // 沒有加速器、剎車或方向盤

void setup() {
 // 初始化按鈕引腳為 INPUT_PULLUP 模式
  pinMode(2, INPUT_PULLUP); // 上按鈕
  pinMode(5, INPUT_PULLUP); // 右按鈕
  pinMode(3, INPUT_PULLUP); // 下按鈕
  pinMode(4, INPUT_PULLUP); // 左按鈕
  pinMode(6, INPUT_PULLUP);  // 按鈕 1
  pinMode(7, INPUT_PULLUP);  // 按鈕 2
  pinMode(8, INPUT_PULLUP);  // 按鈕 3
// 初始化 Joystick 物件
  Joystick.begin();
  Joystick.setXAxis(0);
  Joystick.setYAxis(0);
  Joystick.setXAxisRange(-1, 1);
  Joystick.setYAxisRange(-1, 1);
}

void loop() {
  // 讀取按鈕的狀態
  int upButtonState = digitalRead(2);
  int rightButtonState = digitalRead(5);
  int downButtonState = digitalRead(3);
  int leftButtonState = digitalRead(4);
  int button1State = digitalRead(6);
  int button2State = digitalRead(7);
  int button3State = digitalRead(8);

 

 if (upButtonState == LOW) {
  Joystick.setYAxis(-1); // 上按鈕是下搖桿
}  else if (downButtonState == LOW) {
  Joystick.setYAxis(1); // 下按鈕是上搖桿
} else {
  Joystick.setYAxis(0); // 中
}
 if (leftButtonState == LOW) {
  Joystick.setXAxis(-1); // 上按鈕是下搖桿
}  else if (rightButtonState == LOW) {
  Joystick.setXAxis(1); // 下按鈕是上搖桿
} else {
  Joystick.setXAxis(0); // 中
}
  // 設置按鈕的值
  Joystick.setButton(0, button1State == LOW);
  Joystick.setButton(1, button2State == LOW);
  Joystick.setButton(2, button3State == LOW);
  // 延遲一小段時間，避免過多的 USB 報告
  delay(10);
}

