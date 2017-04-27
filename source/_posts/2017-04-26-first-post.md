title: UAV Q476
---
Q476: Points in Figures: Rectangles
在x-y平面上，給你一些矩形和一些點，請你回答這些點落在哪些矩形內（如果有的話）。另外，在這個問題中，剛好落在邊上的點不視為落在該矩形內。
Input
首先是矩形的資料，每個矩形一列，第1個字元代表圖形的類別（r    代表矩形），接下來有4個數值分別代表該矩形左上角及右下角的座標。矩形的個數不會超過10個。
以一列僅含有一個*代表矩形資料結束。
接下來的每列為一個點的座標，也就是要測試的點。若點座標為9999.9    9999.9代表輸入結束（此點不需輸出）

Output
對每一個測試的點，若其落在某矩形內，則輸出下列格式的訊息：
Point i is contained in figure j
如果某個點沒有落在任何矩形內，則輸出：
Point i is not contained in any figure
請注意：點和矩形的編號是按照他們出現在input的順序。請參考Sample    Output

Sample Input
r 8.5 17.0 25.5 -8.5
r 0.0 10.3 5.5 0.0
r 2.5 12.5 12.5 2.5
*
2.0 2.0
4.7 5.3
6.9 11.2
20.0 20.0
17.6 3.2
-5.2 -7.8
9999.9 9999.9

Sample Output
Point 1 is contained in figure 2
Point 2 is contained in figure 2
Point 2 is contained in figure 3
Point 3 is contained in figure 3
Point 4 is not contained in any figure
Point 5 is contained in figure 1
Point 6 is not contained in any figure

做法：
把表示長方形的左上角座標跟右下角座標放在一個陣列中，要測試的點則放在另一個陣列中。
再用迴圈比對，比對的條件是︰
1.如點的x座標 > 長方形左上角的x座標且點的x座標 < 長方形右下角的x座標，同時點的y座標 > 長方形左上角的y座標且點的y座標 >  長方形右下角的y座標，則該點在長方形內。
2.不符合1的條件就是在長方形外。
程式碼:

{%codeblock lang:java%}
package q476; 

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.ArrayList;
import java.util.List;
 
public class Q476 {
 public static void main(String[] args) {
  BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
  List<Double[]> rectangleList = new ArrayList<Double[]>();
  List<Double[]> pointList = new ArrayList<Double[]>();
   
  String s = null;
  try {
   while(!(s = br.readLine()).equals("*") &amp;&amp; rectangleList.size() != 10) {
    String[] recCoordinates = s.split(" ");
    Double[] rectangle = new Double[4];
     
    rectangle[0] = Double.parseDouble(recCoordinates[1]);
    rectangle[1] = Double.parseDouble(recCoordinates[2]);
    rectangle[2] = Double.parseDouble(recCoordinates[3]);
    rectangle[3] = Double.parseDouble(recCoordinates[4]);
     
    rectangleList.add(rectangle);
   }
    
   while(!(s = br.readLine()).equals("9999.9 9999.9")) {
    String[] pointCoordinates = s.split(" ");
    Double[] point = new Double[2];
     
    point[0] = Double.parseDouble(pointCoordinates[0]);
    point[1] = Double.parseDouble(pointCoordinates[1]);
     
    pointList.add(point);
   }
    
   for(Double[] point : pointList) {
    boolean isIn = false;
     
    for(Double[] rectangle : rectangleList) {
     if((point[0] > rectangle[0] &amp;&amp; point[0] < rectangle[2]) &amp;&amp; (point[1] < rectangle[1] &amp;&amp; point[1] > rectangle[3]) ) {
      System.out.println("Point " + (pointList.indexOf(point) +
         1) + " is contained in figure " + (rectangleList.indexOf(rectangle)
         + 1));
      isIn = true;
     }
    }
    if(isIn == false) {
     System.out.println("Point " + (pointList.indexOf(point) + 1) + " is not contained in any figure");
    }
   }
  } catch (IOException e) {
   // TODO Auto-generated catch block
   e.printStackTrace();
  }
 }
}
{%endcodeblock%}

2013/2/27:最近才發現之前的code有錯，重新放上正確的