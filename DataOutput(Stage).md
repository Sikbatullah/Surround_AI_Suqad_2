
**DataOutput(Stage)** is the final stage in the surround framework. It comes after the stage DataModeling and works as the name suggests. The purpose of this stage is to show the final output of the processed data in the framework. For the example EPL match prediction, the final output of the data can be shown as either of the following
* Graph
* Table

Going through the example, the final output of the prediction becomes the odds of a certain team winning against the other team. 

![](epl/output/compare_result.png)

In this output of the graph we can see the comparison between real and predicted data of team’s chances of winning in different scenario. Here H represents home win, A represents Away win and D represent the chances of draw between two teams.

![](epl/output/confusion_matrix.png)

And this image is the visual representation of the confusion matrix where the chances of Home win, Away win and Draw is predicted.
