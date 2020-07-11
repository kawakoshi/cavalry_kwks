# Blend Sub Mesh Positions -サブメッシュの場所などをブレンドする-

> ブレンドサブメッシュポジションズ

https://docs.cavalry.scenegroup.co/elements/behaviours/blend-sub-mesh-positions

![blendsubmeshpositions01](blendsubmeshpositions.assets/blendsubmeshpositions01.png)

サブメッシュとサブメッシュの間をブレンド補完します。

### 共通属性(Common Attributes +)

**Blend** - 宛先シェイプのパス(Destination Shape)に沿う度合いの割合(%)。

**Destination Shape**(宛先シェイプ) - ブレンドする際、宛先になるシェイプを接続します。

**Time Offset** - シェイプに沿う時間をオフセット(ずらし)します。

### 使用例

![blendsubmeshpositions08](blendsubmeshpositions.assets/blendsubmeshpositions08.gif)

1. Ellipse(円形)シェイプを作成します。
2. Radius(半径)をW=20、H=20に設定します。
3. 円形シェイプを選択し、デュプリケーターをAlt+クリックして複製します。(Duplicator1)
4. 1と2の操作をもう一度繰り返し、Duplicator2を作成します。
   ![blendsubmeshpositions02](blendsubmeshpositions.assets/blendsubmeshpositions02.png)
5. Duplicator1をGrid(Count3,3)に設定します。
   ![blendsubmeshpositions03](blendsubmeshpositions.assets/blendsubmeshpositions03.png)
6. Duplicator2をCircleに設定します。
7. Duplicator2のCountを9にします。
   ![blendsubmeshpositions04](blendsubmeshpositions.assets/blendsubmeshpositions04.png)
8.  Blend Sub Mesh Positionsのビヘイビアを追加します。
9. duplicator2をblendSubMeshPostionのdestinationShapeに接続します。
   ![blendsubmeshpositions05](blendsubmeshpositions.assets/blendsubmeshpositions05.png)
10. blendSubMeshPostionをDuplicator1のdeformersに接続します。
    ![blendsubmeshpositions06](blendsubmeshpositions.assets/blendsubmeshpositions06.png)
11. Duplicator2を非表示にします。
12. Blend Sub Mesh PositionのBlendの数値を動かすと動作します。
    ![blendsubmeshpositions07](blendsubmeshpositions.assets/blendsubmeshpositions07.png)

13. Duplicator2のShape ScaleをX=2.5、Y=2.5にします。そうすることで終点のサイズを変えることもできます。

### サンプルファイル

 [blendsubmeshpositions_sample.cv](blendsubmeshpositions.assets/blendsubmeshpositions_sample.cv) 