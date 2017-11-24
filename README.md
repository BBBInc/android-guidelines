# Android guidelines
본 문서는 BBB Inc 구성원들의 Android 협업을 쉽고 명확하게 진행하기 위한 스타일 가이드입니다. 구성원들의 의사결정에 따라 수시로 변경될 수 있습니다.



## 목차
- [프로젝트 가이드라인](#프로젝트-가이드라인)
  - [프로젝트 시작](#프로젝트-시작)
  - [프로젝트 구조](#프로젝트-구조)
  - [파일 네이밍](#파일-네이밍)
- [코드 가이드라인](#코드-가이드라인)
  - [Java 스타일 규칙](#코드-레이아웃)
  - XML 스타일 규칙
  - Test 스타일 규칙



## 프로젝트 가이드라인


### 프로젝트 시작

#### gitignore

새로운 프로젝트를 시작할 때, 항상 Root 폴더에  **[.gitignore](https://github.com/BBBInc/android-style-guide/blob/master/Downloads/.gitignore)** 을 위치시킵니다.


### 프로젝트 구조

#### 패키지 아키텍쳐
- 패키지는 [`package by features`](https://hackernoon.com/package-by-features-not-layers-2d076df1964d) 로 구성합니다.
- 공유 요소들은 `shared` 패키지 아래 위치시키고, `component` 별로 구분하여 정리합니다.

```java
com.bbbtech.project
├─ database
├─ di
├─ features
│  ├─ feature_a
│  ├─ feature_b
│  └─ shared
│     ├─ adapters
│     ├─ managers
│     └─ views
│        ├─ actionbar
│        ├─ activities
│        ├─ fragments
│        ├─ widgets
│        └─ notifications
├─ network
├─ utils
└─ BaseApplication.java
```


### 파일 네이밍

#### 클래스 파일
클래스명은 UpperCamelCase를 사용합니다.
클래스가 Android Component를 extend할 경우, 클래스명은 Component 이름으로 끝나야 합니다.

`MainActivity`, `LoginFragment`, `AuthAlertDialog`, `ProtocolConnectionService`

#### Resource 파일
Resource 파일명은 lower_underscore를 사용합니다.

##### Drawable 파일
drawables의 경우 Root element의 이름으로 시작합니다.

|Asset Type|Prefix|Example|
|----------|------|-------|
|shape|`shape_`|`shape_oval_white.xml`|
|ripple|`ripple_`|`ripple_btn_login.xml`|
|selector|`selector_`|`selector_item_checkbox.xml`|
|layer-list|`layer_`|`layer_base_progress.xml`|

이미지 파일은 그림 기호의 경우에만 Icon으로 간주하고 `ic`로 시작합니다. View의 배경으로 사용될 경우에는 `bg`, 그 외는 `img`로 시작합니다.

|Asset Type|Prefix|Example|
|----------|------|-------|
|Icons|`ic_`|`ic_launcher.png`|
|Images|`img_`|`img_main_logo`|
|Background|`bg_`|`bg_main`|

##### Layout 파일
Layout 파일명은 관련된 Component로 시작합니다.

|Component|Example Class Name|Example File Name|
|---------|------------------|-----------------|
|Activity|`MainActivity`|`activity_main.xml`|
|Fragement|`ProgressFragment`|`fragment_progress.xml`|
|AdapterView item|---|`item_person.xml`|
|Others|---|`view_login_info`|

##### Menu 파일
menu 파일은 menu 폴더 내에 위치하기 때문에 별도의 prefix 없이 사용되는 Component를 앞으로 보냅니다.

|Example Activity Name|Example File Name|
|---------------------|-----------------|
|`MainActivity`|`activity_main.xml`|

##### Values 파일
Values 폴더 내에 위치한 리소스 파일명은 복수형으로 사용합니다.

`strings.xml`, `colors.xml`, `dimens.xml`, `ui_colors.xml`



## 코드 가이드라인


### 코드 레이아웃

#### 메서드 순서
- Android component를 `@Override` 하는 메서드들은 해당 component의 lifecycle에 맞춘 순서대로 배치합니다.
- lifecycle 이외의 메서드들을 `@Override` 할 경우 lifecyle 메서드 다음 순서로 위치시킵니다.
- 메서드를 `@Override` 하여 사용할 필요가 없는 경우엔 생략합니다.

[Activity Lifecycle](https://developer.android.com/guide/components/activities/activity-lifecycle.html#alc)
```java
public class MainActivity extends Activity {

    @Override
    public void onCreate() {}
   
    @Override
    public void onStart() {}

    @Override
    public void onResume() {}

    @Override
    public void onPause() {}
    
    @Override
    public void onStop() {}

    @Override
    public void onDestroy() {}
    
    @Override
    public void OnActivityResult() {}
    
    ...
    
}
```

[Fragment Lifecycle](https://developer.android.com/guide/components/fragments.html#Creating)
```java
public class MainActivity extends Activity {

    @Override
    public void onAttach() {}

    @Override
    public void onCreate() {}
    
    @Override
    public void onCreateView() {}
   
    @Override
    public void onActivityCreated() {}
    
    @Override
    public void onStart() {}

    @Override
    public void onResume() {}

    @Override
    public void onPause() {}
    
    @Override
    public void onStop() {}
    
    @Override
    public void onDestroyView() {}

    @Override
    public void onDestroy() {}
    
    @Override
    public void onDetach() {}

}
```

#### Local 변수
- Local 변수는 메서드 내에서 사용 되기 직전에 선언합니다.
단, 코드 구조 상 직전에 선언이 어렵다면 메서드 초반에 선언해도 무방합니다.

#### 최대 줄 길이
- 한줄은 최대 120자를 넘지 않도록 합니다.
- AndroidStudio에서 Preferences를 통해 가로 가이드를 조절 할 수 있습니다.
![Image of HowToSetHorizontalGuilde](https://github.com/BBBInc/android-style-guide/blob/master/Screenshots/howToSetHorizontalGuide.png)

#### 빈 줄
- 빈 줄에는 공백(빈칸)이 포함되지 않도록 합니다.
- 모든 파일은 빈 줄로 끝나도록 합니다.
- Local 변수는 선언 시 위, 아래로 1줄의 공백을 넣습니다.

``` java
private void sendStripConnectMessage() {
    final Bundle bundle = new Bundle();

    bundle.putString(“Example”, “Example String”);

    final Message message = Message.obtain();

    message.setData(bundle);
    sendMessage(message);
}
```

- 생성자 선언부 위에는 2줄, 아래에는 1줄의 공백을 넣습니다.

``` java
private String mName;


public Dog(String name) {
	// …
}

public void feedDogFood(int amount) {
	// …
}
```

- Inner Class는 파일 최하단에 위치시키고, 위에는 2줄의 공백을 넣습니다.
- Inner Class끼리는 1줄의 공백을 넣습니다.

``` java
public void feedDogFood(int amount) {
	// …
}

private static class BarkHandler extends Handler {

    final private WeakReference<Dog> mDog;

    public MessageHandler(Dog dog) {
        mDog = new WeakReference<>(dog);
    }

    @Override
    public void handleMessage(Message bark) {
        final Dog dog = mDog.get();
        // …
    }
}

private static class BiteHandler extends Handler {
	// …
}
```

- 분기문의 분기 사이의 간격은 띄우지 않습니다.

``` java
public void analysisAction(final DogAction dogAction) {
        if (bark) {
	        // …
        } else if (bite) {
	        // …
        } else if (sniff) {
	        // …
        }

        // …
    }
```


### 네이밍

#### 변수
- 변수 이름은 lowerCamelCase를 사용합니다.
- 멤버 변수 이름에 접두사<sup>Prefix</sup> `m` 을 붙입니다.
- AndroidStudio에서 Preferences를 통해 Getter/Setter 생성 시에도 m이 처리 되도록 구현 할 수있습니다.
![Image of HowToSetPrefix](https://github.com/BBBInc/android-style-guide/blob/master/Screenshots/howToSetFieldPrefix.png)

- 단, 클래스가 아닌 단순 저장형식(?)으로 사용할 경우에는 Getter/Setter를 사용하지 않으므로, 접두사<sup>Prefix</sup> `m` 을 붙이지 않는다. 또한 이 경우, 모든 멤버 변수는 `public` 으로 둡니다.

#### 상수
- 상수 이름은 ALL_UPPER_CASE를 사용합니다.
- 각 단어는 underscore `_` 로 분리합니다.
- 상수 이름은 부가 설명 없이도 코드를 이해할 수 있게 작성해야 합니다.

**좋은 예**

```java
final int TAX_RATE = 0.03f;
final int WEDNESDAY = 3;
final int DAYS_IN_WEEK = 7;

…중략…

day = (WEDNESDAY + numberOfDays) % DAYS_IN_WEEK;
```

**나쁜 예**

```java
final int texRate;
final int TAXRATE;
final int DaysInWeek;

…중략…

day = (3 + numberOfDays) % 7;
```

#### 약어
- 약어는 lowerCamelCase를 사용합니다.

|Good|Bad|
|----|---|
|userId|userID|
|urlString|URLString|
|html|HTML|
**좋은 예**

#### Colors
- `colors.xml`은 색상 Palette  개념이므로, 색상을 제외하고 다른 것이 들어가면 안된다. `colors.xml`에는 Alpha 값이 포함되지 않은 RGB 값으로 정의하며, Alpha값이 필요한 경우에는 사용하는 곳에서 변경하여 사용하도록 했습니다.
- UI 구성요소 별 색상 지정은 별도의 파일인 `ui_colors.xml`을 생성하여 `colors.xml`의 색상을 매핑하여 사용합니다.
