---
title: VRPose.linearAcceleration
slug: Web/API/VRPose/linearAcceleration
l10n:
  sourceCommit: f7dae62645a2c735ed6f6ed63f664bf279fdfc4b
---

{{APIRef("WebVR API")}}{{Deprecated_Header}}{{Non-standard_Header}}

**`linearAcceleration`** は {{domxref("VRPose")}} インターフェイスの読み取り専用プロパティで、現在の {{domxref("VRPose.timestamp")}} における {{domxref("VRDisplay")}} の直線加速度ベクトルを表す配列を、メートル/秒/秒単位で返します。

> [!NOTE]
> このプロパティは古い [WebVR API](https://immersive-web.github.io/webvr/spec/1.1/) の一部でした。これは [WebXR 機器 API](https://immersive-web.github.io/webxr/) に置き換えられました。

言い換えれば、 `x`、`y`、`z` 軸に沿ったセンサーの現在の加速度です。

## 値

{{jsxref("Float32Array")}} です。または、VRセンサーが直線加速度データを提供できない場合は `null` です。

## 例

```js
// rendering loop for a VR scene
function drawVRScene() {
  // WebVR: Request the next frame of the animation
  vrSceneFrame = vrDisplay.requestAnimationFrame(drawVRScene);

  // Populate frameData with the data of the next frame to display
  vrDisplay.getFrameData(frameData);

  // Retrieve the linear acceleration values for use in rendering
  // curFramePose is a VRPose object
  const curFramePose = frameData.pose;
  const linAcc = curFramePose.linearAcceleration;
  const lax = linAcc[0];
  const lay = linAcc[1];
  const laz = linAcc[2];

  // render the scene
  // …

  // WebVR: submit the rendered frame to the VR display
  vrDisplay.submitFrame();
}
```

## 仕様書

このプロパティは古い [WebVR API](https://immersive-web.github.io/webvr/spec/1.1/) の一部であり、これは [WebXR 機器 API](https://immersive-web.github.io/webxr/) で置き枯れられました。標準規格になる見込みはありません。

すべてのブラウザーが新しい [WebXR API](/ja/docs/Web/API/WebXR_Device_API/Fundamentals) を実装するまで、 [A-Frame](https://aframe.io/)、[Babylon.js](https://www.babylonjs.com/)、[Three.js](https://threejs.org/) などのフレームワークを使用するか、[ポリフィル](https://github.com/immersive-web/webxr-polyfill)を使用することが、すべてのブラウザーで動作する WebXR アプリを開発する上で推奨されます。[\[1\]](https://developer.oculus.com/documentation/web/port-vr-xr/)

## ブラウザーの互換性

{{Compat}}

## 関連情報

- [WebVR API](/ja/docs/Web/API/WebVR_API)