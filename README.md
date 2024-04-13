> [!TIP]
> This project is ready to use!

# React Native Naver Map

[![NPM](https://badge.fury.io/js/@mj-studio%2Freact-native-naver-map.svg)](https://badge.fury.io/js/@mj-studio%2Freact-native-naver-map) [![Android SDK - 3.18.0](https://img.shields.io/badge/Android_SDK-3.18.0-2ea44f)](https://) [![iOS SDK - 3.18.0](https://img.shields.io/badge/iOS_SDK-3.18.0-3522ff)](https://)

---

![rnnm](https://github.com/mj-studio-library/react-native-naver-map/assets/33388801/de8cbe13-1fc7-453b-88a4-41c23a2b2d8b)

리액트 네이티브 [Naver Map](https://www.ncloud.com/product/applicationService/maps) 컴포넌트입니다.

![preview](https://raw.githubusercontent.com/mym0404/image-archive/master/202404101826965.webp)

## 왜 이 라이브러리를 써야하나요?

이 프로젝트는 다음과 같은 목적을 가집니다.

### 1. 더 이상 관리되지 않는 [기존 라이브러리](https://github.com/QuadFlask/react-native-naver-map) 대체

기존 라이브러리의 모든 기능을 가져간 채로 API의 변경도 마이그레이션을 위해 되도록이면 지양하려고 했으나
개선이 필요한 부분들은 필요하다고 생각되면 바꿉니다. 예를 들어, 기존 라이브러리에서 `region`이 잘못 계산되고 있던 버그 등입니다.

Usage는 [`react-native-map`의 Usage](https://github.com/react-native-maps/react-native-maps/blob/master/docs/mapview.md)
를 되도록 따릅니다.

### 2. New Architecture Renderer Fabric 지원

> [!NOTE]
> Fabric을 지원한다고 Old Architecture를 지원하지 않는 것이 아닌 두 Architecture모두에서 작동하는 컴포넌트를 제작합니다.

### 3. Expo 지원

[expo config plugin](https://docs.expo.dev/modules/config-plugin-and-native-module-tutorial/)을 사용해
Expo환경에서도 빌드할 수 있습니다.

Expo Go에선 사용하지
못하지만 [development build](https://docs.expo.dev/develop/development-builds/introduction/), production
환경에서 사용할 수 있습니다.

### 4. 새롭게 만드는 이 라이브러리는 Naver Map SDK의 최신 기능들을 모두 지원합니다

Seamless한 Props와 Command들로 Naver Map을 조작할 수 있습니다.

### 5. 성능 최적화

Event Coalescing를 통해 Native -> JS 로의 이벤트 중 쓸모없는 이벤트들을 걸러내 성능이 최적화가 됩니다.

## Usage

### Install

```shell
# npm
npm install --save @mj-studio/react-native-naver-map

# yarn
yarn add @mj-studio/react-native-naver-map

# expo
npx expo install @mj-studio/react-native-naver-map
```

For ios, you should install pods

### Android

더 자세한 설정은 [공식 문서](https://navermaps.github.io/android-map-sdk/guide-ko/1.html)를 참고해주세요.

#### 1. Maven repository import

Import Naver SDK Maven Repository to `android/build.gradle`.

```groovy
allprojects {
    repositories {
        maven {
            url "https://repository.map.naver.com/archive/maven"
        }
    }
}
```

#### 2. Add Naver SDK key to `AndroidManifest.xml`

```xml
<manifest>
    <application>
        <meta-data
            android:name="com.naver.maps.map.CLIENT_ID"
            android:value="YOUR_CLIENT_ID_HERE" />
    </application>
</manifest>
```

#### 3. (Optional) Request location permission to `AndroidManifest.xml`

Currently, this package will request location permission for showing user's current location.

```xml
<manifest>
    <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
    <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
</manifest>
```

### iOS

더 자세한 설정은 [공식 문서](https://navermaps.github.io/ios-map-sdk/guide-ko/1.html)를 참고해주세요.

#### 1. Set Naver SDK key to `info.plist`

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
...
    <key>NMFClientId</key>
    <string>YOUR_CLIENT_ID_HERE</string>
...
<dict>
<plist>
```

#### 2. (Optional) Set location permission usage description to `info.plist`

Currently, this package will request location permission for showing user's current location.

```xml
<plist version="1.0">
<dict>
    <key>NSLocationAlwaysUsageDescription</key>
    <string>{{your usage description}}</string>
    <key>NSLocationWhenInUseUsageDescription</key>
    <string>{{your usage description}}</string>
</dict>
</plist>
```

### Expo

#### 1. Add `expo-build-properties` package

This is for inject naver maven repository.

```shell
npx expo install expo-build-properties
```

#### 2. Add Config Plugin into `app.json`

```json
{
  ...
  "plugins": [
    [
      "@mj-studio/react-native-naver-map",
      {
        "client_id": "{{Naver Map Client Key}}",
        // (optional)
        "android": {
          "ACCESS_FINE_LOCATION": true,
          "ACCESS_COARSE_LOCATION": true
        },
        // (optional)
        "ios": {
          "NSLocationAlwaysUsageDescription": "{{ your location usage description }}",
          "NSLocationWhenInUseUsageDescription": "{{ your location usage description }}"
        }
      }
    ],
    [
      "expo-build-properties",
      {
        "android": {
          "extraMavenRepos": ["https://repository.map.naver.com/archive/maven"]
        }
      }
    ],
    ...
  ]
}
```

Expo는 위에서 설명된 Android, iOS의 설정법이 필요하지 않습니다.

## Components

> [!NOTE]
> 대부분의 Type들과 Prop들의 설명은 코드의 주석에도 적혀있고 이 프로젝트는 TypeScript를 지원하니 코드에서만 확인해도 사용에 무리가 없을 것입니다.

- ✅ Fully Supported
- ⚠️ Developing, lack of features yet
- 📦 Planned

| Component                                                                                     | iOS | Android | Description   |
|-----------------------------------------------------------------------------------------------|-----|---------|---------------|
| [NaverMapView](https://navermaps.github.io/android-map-sdk/guide-ko/2-3.html)                 | ✅   | ✅       | 지도            |
| [NaverMapMarkerOverlay](https://navermaps.github.io/android-map-sdk/guide-ko/5-2.html)        | ✅   | ✅       | 마커 오버레이       |
| [Info Window](https://navermaps.github.io/android-map-sdk/guide-ko/5-3.html)                  | 📦  | 📦      | 오버레이의 콜오버, 툴팁 |
| [NaverMapCircleOverlay](https://navermaps.github.io/android-map-sdk/guide-ko/5-4.html)        | ✅   | ✅       | 원 오버레이        |
| [NaverMapPolylineOverlay](https://navermaps.github.io/android-map-sdk/guide-ko/5-4.html)      | ✅   | ✅       | 폴리라인 오버레이     |
| [NaverMapPolygonOverlay](https://navermaps.github.io/android-map-sdk/guide-ko/5-4.html)       | ✅   | ✅       | 폴리곤           |
| [NaverMapLocationOverlay](https://navermaps.github.io/android-map-sdk/guide-ko/5-5.html)      | 📦  | 📦      | 커스텀 위치 오버레이   |
| [NaverMapGroundOverlay](https://navermaps.github.io/android-map-sdk/guide-ko/5-6.html)        | 📦  | 📦      | 지상 오버레이       |
| [NaverMapPathOverlay](https://navermaps.github.io/android-map-sdk/guide-ko/5-7.html)          | ✅   | ✅       | 경로 오버레이       |
| [NaverMapMultipartPathOverlay](https://navermaps.github.io/android-map-sdk/guide-ko/5-7.html) | 📦  | 📦      | 여러개의 경로 오버레이  |
| [NaverMapArrowPathOverlay](https://navermaps.github.io/android-map-sdk/guide-ko/5-7.html)     | 📦  | 📦      | 화살표 경로 오버레이   |

## Props & Commands

- ✅ Done
- 📦 Planned
- ❓ Maybe Planned
- ❌ Not Planned

### `NaverMapView`

#### Props

| Prop                     | iOS | Android | Type    | Default       | Description                           |
|--------------------------|-----|---------|---------|---------------|---------------------------------------|
| mapType                  | ✅   | ✅       |         |               |                                       |
| layerGroups              | ✅   | ✅       |         |               |                                       |
| camera                   | ✅   | ✅       |         |               |                                       |
| initialCamera            | ✅   | ✅       |         |               |                                       |
| region                   | ✅   | ✅       |         |               |                                       |
| initialRegion            | ✅   | ✅       |         |               |                                       |
| isIndoorEnabled          | ✅   | ✅       |         |               |                                       |
| isNightModeEnabled       | ✅   | ✅       |         |               |                                       |
| isLiteModeEnabled        | ✅   | ✅       |         |               |                                       |
| lightness                | ✅   | ✅       |         |               |                                       |
| buildingHeight           | ✅   | ✅       |         |               |                                       |
| symbolScale              | ✅   | ✅       |         |               |                                       |
| symbolPerspectiveRatio   | ✅   | ✅       |         |               |                                       |
| mapPadding               | ✅   | ✅       |         |               |                                       |
| isShowCompass            | ✅   | ✅       |         |               |                                       |
| isShowScaleBar           | ✅   | ✅       |         |               |                                       |
| isShowZoomControls       | ✅   | ✅       |         |               |                                       |
| isShowIndoorLevelPicker  | ✅   | ✅       |         |               |                                       |
| minZoom                  | ✅   | ✅       |         |               |                                       |
| maxZoom                  | ✅   | ✅       |         |               |                                       |
| extent                   | ✅   | ✅       |         |               |                                       |
| isExtentBoundedInKorea   | ✅   | ✅       |         |               |                                       |
| logoAlign                | ✅   | ✅       |         |               |                                       |
| logoMargin               | ✅   | ✅       |         |               |                                       |
| isLogoInteractionEnabled | ❌   | ❌       |         |               |                                       |
| isScrollGesturesEnabled  | ✅   | ✅       |         |               |                                       |
| isZoomGesturesEnabled    | ✅   | ✅       |         |               |                                       |
| isTiltGesturesEnabled    | ✅   | ✅       |         |               |                                       |
| isRotateGesturesEnabled  | ✅   | ✅       |         |               |                                       |
| isStopGesturesEnabled    | ✅   | ✅       |         |               |                                       |
| isShowLocationButton     | ✅   | ✅       |         |               |                                       |
| isUseTextureViewAndroid  | ❌   | ✅       |         |               |                                       |
| markerClustering         | 📦  | 📦      |         |               |                                       |
| fpsLimit                 | 📦  | 📦      |         |               |                                       |
| gestureFrictions         | 📦  | 📦      |         |               |                                       |
| locale                   | ✅   | ✅       | String? | system locale | 지도의 언어를 지정합니다, e.g.) `ja`, `ko`, `en` |

#### Events

| Event            | iOS | Android | Type | Description |
|------------------|-----|---------|------|-------------|
| onInitialized    | ✅   | ✅       |      |             |
| onOptionChanged  | ✅   | ✅       |      |             |
| onCameraChanged  | ✅   | ✅       |      |             |
| onTapMap         | ✅   | ✅       |      |             |
| onTapSymbol      | 📦  | 📦      |      |             |
| onAuthFailed     | ❌   | ❌       |      |             |
| onLocationChange | 📦  | 📦      |      |             |

#### Commands

| Command                    | iOS | Android | Type | Description |
|----------------------------|-----|---------|------|-------------|
| animateCameraTo            | ✅   | ✅       |      |             |
| animateCameraBy            | ✅   | ✅       |      |             |
| animateRegionTo            | ✅   | ✅       |      |             |
| animateCameraWithTwoCoords | ✅   | ✅       |      |             |
| cancelAnimation            | ✅   | ✅       |      |             |
| screenToCoordinate         | 📦  | 📦      |      |             |
| coordinateToScreen         | 📦  | 📦      |      |             |
| clusterMarkers             | 📦  | 📦      |      |             |
| setLocationTrackingMode    | ✅   | ✅       |      |             |

### Marker Common

#### Props

| Prop               | iOS | Android | Type | Default | Description |
|--------------------|-----|---------|------|---------|-------------|
| latitude           | ✅   | ✅       |      |         |             |
| longitude          | ✅   | ✅       |      |         |             |
| zIndex             | ✅   | ✅       |      |         |             |
| isHidden           | ✅   | ✅       |      |         |             |
| minZoom            | ✅   | ✅       |      |         |             |
| maxZoom            | ✅   | ✅       |      |         |             |
| isMinZoomInclusive | ✅   | ✅       |      |         |             |
| isMaxZoomInclusive | ✅   | ✅       |      |         |             |

#### Events

|           | iOS | Android | Type | Description |
|-----------|-----|---------|------|-------------|
| onTap     | ✅   | ✅       |      |             |
| onLongTap | ❌   | 📦      |      |             |

### `NaverMapMarkerOverlay`

#### 마커의 종류와 성능

마커의 종류는 총 네가지입니다.

1. Default Symbol (green, red, gray, ...) (caching ✅)

```js
image={'green'}
```

2. Local Resource (`ImageSourcePropType` of react native) (caching ✅)

이는 추후에 더 나은 성능을 위해 Android, iOS native resource를 사용해 screen density에 따라 최적의 마커가 선택되게 할 수 있는 로직을 구현하려
합니다.

```js
image={require('./marker.png')}
```

3. Network Image (caching ✅)

```js
image={{uri: 'https://example.com/image.png'}}
```

> [!WARNING]
> 현재 header auth같은 객채 내의 다른 속성은 지원되지 않습니다.

4. Custom React View (caching ❌)

iOS에선 현재 View들에 `collapsible=false`를 설정해야 동작할 것입니다.

```tsx
<NaverMapMarkerOverlay width={100} height={100} ...>
  <View collapsible={false} style={{width: 100, height: 100}}>
    ...
  </View>
</NaverMapMarkerOverlay>
```

> [!IMPORTANT]
> 이 타입은 많이 생성될 시 성능에 굉장히 영향을 미칠 수 있습니다.
> 아직은 단순하게만 사용하시거나 되도록이면 이미지를 사용하는 것을 추천드립니다.

현재 이 타입은 Android에선 `react-native-map`의 구현체를 비슷하게 가져와 React Native의 Shadow Node를 조금 커스텀해서 자식의 위치를
추적한다음 실제 Android의 `View`를 삽입해줍니다.

iOS에선 단순히 `UIView`를 `UIImage`로 캔버스에 그려 표시해줍니다.

두 방법 모두가 이미지 캐싱이 아직 지원되지 않고(추후에 `reuseableIdentifier`같은 속성으로 지원이 가능할 것으로 보입니다), 마커 하나당 많은 리소스를 차지하게
됩니다.

#### Props

| Prop                      | iOS                                                | Android | Type | Default | Description |
|---------------------------|----------------------------------------------------|---------|------|---------|-------------|
| width                     | ✅                                                  | ✅       |      |         |             |
| height                    | ✅                                                  | ✅       |      |         |             |
| anchor                    | ✅                                                  | ✅       |      |         |             |
| angle                     | ✅                                                  | ✅       |      |         |             |
| isFlatEnabled             | ✅                                                  | ✅       |      |         |             |
| isIconPerspectiveEnabled  | ✅                                                  | ✅       |      |         |             |
| alpha                     | ✅                                                  | ✅       |      |         |             |
| isHideCollidedSymbols     | ✅                                                  | ✅       |      |         |             |
| isHideCollidedMarkers     | ✅                                                  | ✅       |      |         |             |
| isHideCollidedCaptions    | ✅                                                  | ✅       |      |         |             |
| isForceShowIcon           | ✅                                                  | ✅       |      |         |             |
| tintColor                 | ✅                                                  | ✅       |      |         |             |
| image(default symbols)    | ✅                                                  | ✅       |      |         |             |
| image(local image)        | ✅                                                  | ✅       |      |         |             |
| image(network image)      | ✅                                                  | ✅       |      |         |             |
| image(custom view)        | (new arch ✅) (old arch 📦, not a techinical issue) | ✅       |      |         |             |
| caption                   | ✅                                                  | ✅       |      |         |             |
| caption-key               | ✅                                                  | ✅       |      |         |             |
| caption-text              | ✅                                                  | ✅       |      |         |             |
| caption-requestedWidth    | ✅                                                  | ✅       |      |         |             |
| caption-align             | ✅                                                  | ✅       |      |         |             |
| caption-offset            | ✅                                                  | ✅       |      |         |             |
| caption-color             | ✅                                                  | ✅       |      |         |             |
| caption-haloColor         | ✅                                                  | ✅       |      |         |             |
| caption-textSize          | ✅                                                  | ✅       |      |         |             |
| caption-minZoom           | ✅                                                  | ✅       |      |         |             |
| caption-maxZoom           | ✅                                                  | ✅       |      |         |             |
| caption-fontFamily        | ❓                                                  | ❓       |      |         |             |
| subcaption                | ✅                                                  | ✅       |      |         |             |
| subcaption-key            | ✅                                                  | ✅       |      |         |             |
| subcaption-text           | ✅                                                  | ✅       |      |         |             |
| subcaption-color          | ✅                                                  | ✅       |      |         |             |
| subcaption-haloColor      | ✅                                                  | ✅       |      |         |             |
| subcaption-textSize       | ✅                                                  | ✅       |      |         |             |
| subcaption-requestedWidth | ✅                                                  | ✅       |      |         |             |
| subcaption-minZoom        | ✅                                                  | ✅       |      |         |             |
| subcaption-maxZoom        | ✅                                                  | ✅       |      |         |             |
| subcaption-fontFamily     | ❓                                                  | ❓       |      |         |             |

### `NaverMapPolylineOverlay`

#### Props

| Prop     | iOS | Android | Type | Default | Description |
|----------|-----|---------|------|---------|-------------|
| coords   | ✅   | ✅       |      |         |             |
| width    | ✅   | ✅       |      |         |             |
| color    | ✅   | ✅       |      |         |             |
| pattern  | ✅   | ✅       |      |         |             |
| capType  | ✅   | ✅       |      |         |             |
| joinType | ✅   | ✅       |      |         |             |

### `NaverMapPathOverlay`

#### Props

| Prop                   | iOS | Android | Type | Default | Description |
|------------------------|-----|---------|------|---------|-------------|
| coords                 | ✅   | ✅       |      |         |             |
| width                  | ✅   | ✅       |      |         |             |
| outlineWidth           | ✅   | ✅       |      |         |             |
| patternImage           | 📦  | 📦      |      |         |             |
| patternInterval        | ✅   | ✅       |      |         |             |
| progress               | ✅   | ✅       |      |         |             |
| color                  | ✅   | ✅       |      |         |             |
| passedColor            | ✅   | ✅       |      |         |             |
| outlineColor           | ✅   | ✅       |      |         |             |
| passedOutlineColor     | ✅   | ✅       |      |         |             |
| isHideCollidedSymbols  | ✅   | ✅       |      |         |             |
| isHideCollidedMarkers  | ✅   | ✅       |      |         |             |
| isHideCollidedCaptions | ✅   | ✅       |      |         |             |

### `NaverMapCircleOverlay`

#### Props

| Prop         | iOS | Android | Type | Default | Description |
|--------------|-----|---------|------|---------|-------------|
| radius       | ✅   | ✅       |      |         |             |
| color        | ✅   | ✅       |      |         |             |
| outlineWidth | ✅   | ✅       |      |         |             |
| outlineColor | ✅   | ✅       |      |         |             |

### `NaverMapPolygonOverlay`

#### Props

| Prop         | iOS | Android | Type | Default | Description |
|--------------|-----|---------|------|---------|-------------|
| coords       | ✅   | ✅       |      |         |             |
| holes        | ✅   | ✅       |      |         |             |
| color        | ✅   | ✅       |      |         |             |
| outlineWidth | ✅   | ✅       |      |         |             |
| outlineColor | ✅   | ✅       |      |         |             |

### Types

#### Coord

Coord는 하나의 위경도 좌표를 나타내는 객체입니다.
latitude 속성이 위도를, longitude 속성이 경도를 나타냅니다.

|           | Type   | Default | Description |
|-----------|--------|---------|-------------|
| latitude  | number |         | 위도          |
| longitude | number |         | 경도          |

#### Rect

사각형을 의미합니다.


|         | Type   | Default | Description |
|---------|--------|---------|-------------|
| left    | number |         |             |
| top     | number |         |             |
| right   | number |         |             |
| bottom  | number |         |             |


#### Align

정렬 위치입니다.

- Center
- Left
- Right
- Top
- Bottom
- TopLeft
- TopRight
- BottomRight
- BottomLeft

#### LogoAlign

네이버 로고의 정렬 위치입니다.

- TopLeft
- TopRight
- BottomRight
- BottomLeft

#### Camera

현재 카메라의 상태를 나타내는 객체입니다.

|           | Type   | Default | Description                                                                                                                                                                                                                                                               |
|-----------|--------|---------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| latitude  | number |         | 위도                                                                                                                                                                                                                                                                        |
| longitude | number |         | 경도                                                                                                                                                                                                                                                                        |
| zoom      | number |         | 카메라의 줌 레벨을 나타내는 속성입니다.<br/>줌 레벨은 지도의 축척을 나타냅니다.<br/>즉, 줌 레벨이 작을수록 지도가 축소되고 클수록 확대됩니다. 줌 레벨이 커지면 지도에 나타나는 정보도 더욱 세밀해집니다.                                                                                                                                                   |
| tilt      | number |         | 카메라의 기울임 각도를 나타내는 속성입니다.<br/>카메라는 기울임 각도만큼 지면을 비스듬하게 내려다봅니다.<br/>기울임 각도가 0도이면 카메라가 지면을 수직으로 내려다보며, 각도가 증가하면 카메라의 시선도 점점 수평에 가깝게 기울어집니다.<br/>따라서 기울임 각도가 클수록 더 먼 곳을 볼 수 있게 됩니다.<br/>카메라가 기울어지면 화면에 보이는 지도에 원근감이 적용됩니다.<br/>즉, 화면의 중심을 기준으로 먼 곳은 더 작게 보이고 가까운 곳은 더 크게 보입니다. |
| bearing   | number |         | 카메라의 헤딩 각도를 나타내는 속성입니다.<br/>헤딩은 카메라가 바라보는 방위를 의미합니다.<br/>카메라가 정북 방향을 바라볼 때 헤딩 각도는 0도이며, 시계 방향으로 값이 증가합니다.<br/>즉, 동쪽을 바라볼 때 90도, 남쪽을 바라볼 때 180도가 됩니다.                                                                                                                      |

#### Region

지도에 보이는 위치의 상태를 의미하는 객체입니다.

|                | Type             | Default | Description                                           |
|----------------|------------------|---------|-------------------------------------------------------|
| latitude       | number           |         | 위도, 대개 더 작은 위도 값이며 정확히는 south-west 지점의 latitude 입니다.  |
| longitude      | number           |         | 경도, 대개 더 작은 경도 값이며 정확히는 south-west 지점의 longitude 입니다. |
| latitudeDelta  | number(positive) |         | north-east 지점의 latitude와 latitude와의 위도차이 입니다.         |
| longitudeDelta | number(positive) |         | north-east 지점의 longitude와 longitude와의 경도차이 입니다.       |


#### CameraAnimationEasing

카메라 애니메이션의 Easing입니다.

- EaseIn: 부드럽게 가속하며 이동합니다. 가까운 거리를 이동할 때 적합합니다.
- EaseOut: 부드럽게 감속하며 이동합니다. 가까운 거리를 이동할 때 적합합니다.
- None: 애니메이션 없이 이동합니다.
- Linear: 일정한 속도로 이동합니다.
- Fly: 부드럽게 축소됐다가 확대되며 이동합니다. 먼 거리를 이동할 때 적합합니다.

#### CameraChangeReason

카메라의 위치가 변한 이유입니다.

- Developer: 개발자가 API를 호출해 카메라가 움직였음을 나타냅니다. 기본값입니다.
- Gesture: 사용자의 제스처로 인해 카메라가 움직였음을 나타냅니다.
- Control: 사용자의 버튼 선택으로 인해 카메라가 움직였음을 나타냅니다.
- Location: 위치 트래킹 기능으로 인해 카메라가 움직였음을 나타냅니다.

#### CapType

- Round
- Butt
- Square

#### JoinType

- Round
- Bevel
- Miter

#### LocationTrackingMode

사용자의 위치를 추적하는 모드입니다.

- None: 위치를 추적하지 않습니다.
- NoFollow: 위치 추적이 활성화되고, 현위치 오버레이가 사용자의 위치를 따라 움직입니다. 그러나 지도는 움직이지 않습니다.
- Follow: 위치 추적이 활성화되고, 현위치 오버레이와 카메라의 좌표가 사용자의 위치를 따라 움직입니다.  API나 제스처를 사용해 임의로 카메라를 움직일 경우 모드가 NoFollow로 바뀝니다.
- Face: 위치 추적이 활성화되고, 현위치 오버레이, 카메라의 좌표, 베어링이 사용자의 위치 및 방향을 따라 움직입니다. API나 제스처를 사용해 임의로 카메라를 움직일 경우 모드가 NoFollow로 바뀝니다.

#### MapType

지도의 유형을 변경하면 가장 바닥에 나타나는 배경 지도의 스타일이 변경됩니다.

- Basic: 일반 지도입니다. 하천, 녹지, 도로, 심벌 등 다양한 정보를 노출합니다.
- Navi: 차량용 내비게이션에 특화된 지도입니다.
- Satellite: 위성 지도입니다. 심벌, 도로 등 위성 사진을 제외한 요소는 노출되지 않습니다.
- Hybrid: 위성 사진과 도로, 심벌을 함께 노출하는 하이브리드 지도입니다.
- NaviHybrid: 위성 사진과 내비게이션용 도로, 심벌을 함께 노출하는 하이브리드 지도입니다.
- Terrain: 지형도입니다. 산악 지형을 실제 지형과 유사하게 입체적으로 표현합니다.
- None: 지도를 나타내지 않습니다. 단, 오버레이는 여전히 나타납니다.


## Supporting Table - Architecture

|        | iOS | Android |
|--------|-----|---------|
| Bridge | ✅   | ✅       |
| Fabric | ✅️  | ✅️      |

## Milestone

- [x] Project Started (23.04.01)
- [x] Project Setup & Component Structure (23.04.03)
- [x] General Props & Commands (23.04.05)
- [x] Camera, Region, Commands, Events (23.04.07)
- [x] Implement Basic Overlays (23.04.10)
- [x] Location Service (23.04.10)
- [x] Support Paper(Old Arch) (23.04.11)
- [x] Release (23.04.11)
- [x] Support Expo with config plugin (23.04.12)
- [x] Docs
- [ ] Implement Advanced Overlays <- 🔥

## Contributing

See the [contributing guide](CONTRIBUTING.md) to learn how to contribute to the repository and the
development workflow.

## License

MIT
