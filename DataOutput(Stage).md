# DataOutput(Stage)
**DataOutput(Stage)** is the final stage in the surround framework. It comes after the stage DataModeling and works as the name suggests. The purpose of this stage is to show the final output of the processed data in the framework. For the example EPL match prediction, the final output of the data can be shown as either of the following
* Graph
* Table

The DataOutput(Stage) can be farther broken down to three different parts.

#### display_histogram
```
def display_histogram(self, histo_data, output_dir):

        fig1, ax = plt.subplots(1, 2)
        histo_data.FTR.value_counts().plot("bar", ax=ax[0]).set_title("Real")
        histo_data.Predicted_FTR.value_counts().plot("bar", ax=ax[1]).set_title("Predicted")
        plt.show()

        fig1.savefig(output_dir + "/compare_result.png")
        plt.close()
```
From the code we can see that `plt` is the called function `matplotlib.pyplot` which is responsible for plotting the histogram. And the `histo_data` is the data derived from the previous classes to graphically represent the predection bars. The output we get from  `display_histogram` is given below

![](epl/output/compare_result.png)

#### prediction_report
```
def prediction_report(self, real, prediction, output_dir):
        h = 0
        a = 0
        d = 0
        for x in prediction:
            if x == "H":
                h = h + 1
            elif x == "A":
                a = a + 1
            else:
                d = d + 1
        print("Total home win: {0}".format(h))
        print("Total away win: {0}".format(a))
        print("Total draw: {0}".format(d))

        labels = ["H", "D", "A"]
        cnf_matrix = metrics.confusion_matrix(real, prediction, labels)
        print(cnf_matrix)
        print("The accuracy of the Logistic regression model is: {0}" .format(metrics.accuracy_score(real, prediction)))

        df_confusion = pd.DataFrame(cnf_matrix, index=["Home Win", "Draw", "Away Win"], columns=["Predicted Home Win", "Predicted Draw", "Predicted Away Win"])

        fig2 = plt.figure(2)
        sns.heatmap(df_confusion, annot=True, cbar=False)
        fig2.savefig(output_dir + "/confusion_matrix.png")
        plt.show()
```
From the code above we can see that `sns` is the called function for `seaborn` which is responsible for plotting the confusion matrix. The confusion matrix compares the real data with the predicted data. Here H represents home win, A represents Away win and D represent the chances of draw between two teams.

![](epl/output/confusion_matrix.png)

#### operate
``` def operate(self, surround_data, config):
        output_dir = config.get_path("surround.path_to_output")
        surround_data.result_data.to_csv(output_dir + "/test_output.csv")

        self.display_histogram(surround_data.result_data, output_dir)
        self.prediction_report(surround_data.result_data.FTR, surround_data.result_data.Predicted_FTR, output_dir)
        print("It's fine up to here.")
```
Operate is responsible changing saving the predictive out test cases to the output folder in csv formats. It is also resposnible for the plotting and saving histograms along with plotting confusion matrix and saving the files.
