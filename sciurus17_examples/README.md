[English](README.en.md) | [日本語](README.md)

# sciurus17_examples

Sciurus17のためのパッケージ、 `sciurus17` で用いるサンプルをまとめたパッケージです。

## システムの起動方法

Sciurus17の頭部カメラ、胸部カメラ、制御信号の各ケーブルを制御用パソコンへ接続します。  
本体の電源をONにしカメラが接続されていることを確認します。  
Terminalを開き、 `sciurus17_bringup` の `sciurus17_bringup.launch` を起動します。このlaunchファイルには次のオプションが用意されています。

- use_rviz (default: true)  
Rvizを使用する/使用しない
- use_head_camera (default: true)  
頭部カメラを使用する/使用しない
- use_chest_camera (default: true)  
胸部カメラを使用する/使用しない

### シミュレータを使う場合

実機無しで動作を確認する場合、制御信号のケーブルを接続しない状態で次のコマンドを実行します。  

```
roslaunch sciurus17_bringup sciurus17_bringup.launch
```

### 実機を使う場合

実機で動作を確認する場合、制御信号のケーブルを接続し取り扱い説明書に従いモータパワーをONにした状態で次のコマンドを実行します。  

```
roslaunch sciurus17_bringup sciurus17_bringup.launch
```

### カメラを使用しない場合

次のようにオプションを指定するとカメラを使用しない状態で起動します。

```
roslaunch sciurus17_bringup sciurus17_bringup.launch use_head_camera:=false use_chest_camera:=false
```

### rvizを使用しない場合

次のようにオプションを指定するとrvizによる画面表示を使用しない状態で起動します。画面表示を省略することで制御用パソコンの負荷を下げることができます。  

```
roslaunch sciurus17_bringup sciurus17_bringup.launch use_rviz:=false
```

### Gazeboを使う場合

次のコマンドで起動します。実機との接続やsciurus17_bringupの実行は必要ありません。

```sh
roslaunch sciurus17_gazebo sciurus17_with_table.launch

# rvizを使用しない場合
roslaunch sciurus17_gazebo sciurus17_with_table.launch use_rviz:=false
```

## Run Examples

`sciurus17_bringup.launch`を実行している状態で各サンプルを実行できます。  

- [gripper_action_example](#gripper_action_example)
- [neck_joint_trajectory_example](#neck_joint_trajectory_example)
- [waist_joint_trajectory_example](#waist_joint_trajectory_example)
- [pick_and_place_demo](#pick_and_place_demo)
- [hand_position_publisher](#hand_position_publisher)
- [head_camera_tracking](#head_camera_tracking)
- [chest_camera_tracking](#chest_camera_tracking)
- [depth_camera_tracking](#depth_camera_tracking)
- [preset_pid_gain_example](#preset_pid_gain_example)
- [box_stacking_example](#box_stacking_example)

### gripper_action_example

両腕のハンドを開閉させるコード例です。   
次のコマンドで26度まで開いて閉じる動作を実行します。

```
rosrun sciurus17_examples gripper_action_example.py
```

<img src= https://rt-net.github.io/images/sciurus17/gazebo_gripper_example.gif width=500px />

#### Videos

[![](http://img.youtube.com/vi/iTAAUA_fRXw/sddefault.jpg)](https://youtu.be/iTAAUA_fRXw)

[![](http://img.youtube.com/vi/55YOCixB9VI/sddefault.jpg)](https://youtu.be/55YOCixB9VI)

[back to example list](#run-examples)

---

### neck_joint_trajectory_example

首の角度を変更するコード例です。
次のコマンドで頭を上下左右へ向ける動作を実行します。

```
rosrun sciurus17_examples neck_joint_trajectory_example.py
```

<img src = https://rt-net.github.io/images/sciurus17/gazebo_neck_example.gif width = 500px />

#### Videos

[![](http://img.youtube.com/vi/_4J5bpFNQuI/sddefault.jpg)](https://youtu.be/_4J5bpFNQuI)

[![](http://img.youtube.com/vi/scge_3v7-EA/sddefault.jpg)](https://youtu.be/scge_3v7-EA)

[back to example list](#run-examples)

---

### waist_joint_trajectory_example

腰の角度を変更するコード例です。
次のコマンドで腰を左右へひねる動作を実行します。

```
rosrun sciurus17_examples waist_joint_trajectory_example.py
```

<img src = https://rt-net.github.io/images/sciurus17/gazebo_waist_example.gif width = 500px />

### Videos

[![](http://img.youtube.com/vi/sxu-kN4Qc-o/sddefault.jpg)](https://youtu.be/sxu-kN4Qc-o)

[back to example list](#run-examples)

---

### pick_and_place_demo

右手でターゲットを掴んで動かすデモ動作を次のコマンドで実行します。腰の回転も使用します。

```
rosrun sciurus17_examples pick_and_place_right_arm_demo.py
```

<img src = https://rt-net.github.io/images/sciurus17/gazebo_pick_and_place_right.gif width = 500px />

左手でターゲットを掴んで動かすデモ動作を次のコマンドで実行します。

```
rosrun sciurus17_examples pick_and_place_left_arm_demo.py
```
<img src = https://rt-net.github.io/images/sciurus17/gazebo_pick_and_place_left.gif width = 500px />

両手でターゲットを掴んで動かすデモ動作を次のコマンドで実行します。

```
rosrun sciurus17_examples pick_and_place_two_arm_demo.py
```

<img src = https://rt-net.github.io/images/sciurus17/gazebo_pick_and_place_two.gif width = 500px />

#### Videos

[![](http://img.youtube.com/vi/kjaiWhr-dLg/sddefault.jpg)](https://youtu.be/kjaiWhr-dLg)

[![](http://img.youtube.com/vi/UycaNEHWbv8/sddefault.jpg)](https://youtu.be/UycaNEHWbv8)

[![](http://img.youtube.com/vi/GgKYfSm1NY4/hqdefault.jpg)](https://youtu.be/xo3OiJgu7wg)

[back to example list](#run-examples)

---

### hand_position_publisher

tfの機能でリンク位置を求めるノード例です。  
l_link7とr_link7について、base_linkを基準とした座標をそれぞれ`/sciurus17/hand_pos/left`トピックと
`/sciurus17/hand_pos/right`トピックへ配信します。  
次のコマンドでノードを起動します。  

```
rosrun sciurus17_examples hand_position_publisher_example.py
```

[back to example list](#run-examples)

---

### head_camera_tracking

頭のカメラを使うコード例です。
OpenCVを使ってボール追跡と顔追跡をします。

次のコマンドでOpenCVのPythonライブラリをインストールしてください。
```sh
pip2 install opencv-python
```

次のコマンドでノードを起動します。
```sh
rosrun sciurus17_examples head_camera_tracking.py
```

*ボール追跡をする場合*

[`./scripts/head_camera_tracking.py`](./scripts/head_camera_tracking.py)を編集します。

```python
def _image_callback(self, ros_image):
    # ~~~ 省略 ~~~

        # オブジェクト(特定色 or 顔) の検出
        output_image = self._detect_orange_object(input_image)
        # output_image = self._detect_blue_object(input_image)
        # output_image = self._detect_face(input_image)
```

<img src = https://rt-net.github.io/images/sciurus17/gazebo_head_camera.gif width = 500px />

*顔追跡をする場合*

[`./scripts/head_camera_tracking.py`](./scripts/head_camera_tracking.py)を編集します。

顔追跡にはカスケード型分類器を使用します。

カスケードファイルのディレクトリを設定してください。
**USER_NAME** は環境に合わせて書き換えてください。

```python
class ObjectTracker:
    def __init__(self):
        # ~~~ 省略 ~~~

        # カスケードファイルの読み込み
        # 例
        # self._face_cascade = cv2.CascadeClassifier("/home/USER_NAME/.local/lib/python2.7/site-packages/cv2/data/haarcascade_frontalface_alt2.xml")
        # self._eyes_cascade = cv2.CascadeClassifier("/home/USER_NAME/.local/lib/python2.7/site-packages/cv2/data/haarcascade_eye.xml")
        self._face_cascade = cv2.CascadeClassifier("/home/USER_NAME/.local/lib/python2.7/site-packages/cv2/data/haarcascade_frontalface_alt2.xml")
        self._eyes_cascade = cv2.CascadeClassifier("/home/USER_NAME/.local/lib/python2.7/site-packages/cv2/data/haarcascade_eye.xml")
```

```python
def _image_callback(self, ros_image):
    # ~~~ 省略 ~~~

        # オブジェクト(特定色 or 顔) の検出
        # output_image = self._detect_orange_object(input_image)
        # output_image = self._detect_blue_object(input_image)
        output_image = self._detect_face(input_image)
```


#### Videos

[![](http://img.youtube.com/vi/W39aswfINNU/sddefault.jpg)](https://youtu.be/W39aswfINNU)

[![](http://img.youtube.com/vi/I67OD25NkMg/sddefault.jpg)](https://youtu.be/I67OD25NkMg)

動画で使用しているボールは、アールティショップの
[こちらのページ](https://www.rt-shop.jp/index.php?main_page=product_info&cPath=1299_1307&products_id=3701)
で購入できます。

[back to example list](#run-examples)

---

### chest_camera_tracking

胸のカメラを使うコード例です。
OpenCVを使ってボール追跡をします。

次のコマンドでOpenCVのPythonライブラリをインストールしてください。
```sh
pip2 install opencv-python
```

次のコマンドでノードを起動します。
```sh
rosrun sciurus17_examples chest_camera_tracking.py
```

<img src = https://rt-net.github.io/images/sciurus17/gazebo_chest_camera.gif width = 500px />

*顔追跡とボール追跡の同時実行*

頭カメラと胸のカメラの両方を使って、顔追跡とボール追跡をします。

```sh
rosrun sciurus17_examples head_camera_tracking.py

# 別のターミナルで実行
rosrun sciurus17_examples chest_camera_tracking.py
```

#### Videos

[![](http://img.youtube.com/vi/wscw-I4wCaM/sddefault.jpg)](https://youtu.be/wscw-I4wCaM)

[![](http://img.youtube.com/vi/c81I0GaC2DU/sddefault.jpg)](https://youtu.be/c81I0GaC2DU)

[back to example list](#run-examples)

---

### depth_camera_tracking

頭の深度カメラを使うコード例です。
指定深度内の物体を追跡します。

次のコマンドでOpenCVのPythonライブラリをインストールしてください。
```sh
pip2 install opencv-python
```

次のコマンドでノードを起動します。
```sh
rosrun sciurus17_examples depth_camera_tracking.py
```

デフォルトでは検出範囲を4段階に分けています。
検出範囲を変更する場合は[`./scripts/depth_camera_tracking.py`](./scripts/depth_camera_tracking.py)を編集します。

```python
    def _detect_object(self, input_depth_image):
        # 検出するオブジェクトの大きさを制限する
        MIN_OBJECT_SIZE = 10000 # px * px
        MAX_OBJECT_SIZE = 80000 # px * px

        # 検出範囲を4段階設ける
        # 単位はmm
        DETECTION_DEPTH = [
                (500, 700),
                (600, 800),
                (700, 900),
                (800, 1000)]
```

[back to example list](#run-examples)

---

### preset_pid_gain_example

`sciurus17_control`の`preset_reconfigure`を使うコード例です。
サーボモータのPIDゲインを一斉に変更できます。

プリセットは[sciurus17_control/scripts/preset_reconfigure.py](../sciurus17_control/scripts/preset_reconfigure.py)
にて編集できます。

次のコマンドを実行すると、`preset_reconfigure.py`と`preset_pid_gain_example.py`のノードを起動します。

```sh
roslaunch sciurus17_examples preset_pid_gain_example.launch
```

[back to example list](#run-examples)

---

### box_stacking_example

<img src = https://rt-net.github.io/images/sciurus17/gazebo_box_stacking.gif width = 500px />

[PointCloudLibrary](http://pointclouds.org/)を用いて箱を検出し、箱を積み重ねるコード例です。

次のコマンドでノードを起動します。

```sh
roslaunch sciurus17_examples box_stacking_example.launch
```

RVizで`visualization_msgs/MarkerArray`の`/sciurus17/example/markers`を表示すると検出した箱を確認できます。

<img src = https://rt-net.github.io/images/sciurus17/rviz_box_stacking.png width = 500px />

#### Videos

[![](http://img.youtube.com/vi/nKMjBNcgDS4/sddefault.jpg)](https://youtu.be/nKMjBNcgDS4)

[back to example list](#run-examples)
