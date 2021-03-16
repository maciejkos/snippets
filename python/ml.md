#python #ml 
machine learning snippets  

```python
from sklearn.model_selection import train_test_split
X_train,X_test,y_train,y_test=train_test_split(features,labels,test_size=0.25,random_state=0) # X: features, y: labels

# evaluate

from sklearn.metrics import classification_report
print(classification_report(ytest, yfit, target_names=features))

y_pred=my_model.predict(X_test)

print("Accuracy:",metrics.accuracy_score(y_test, y_pred))
print("Precision:",metrics.precision_score(y_test, y_pred))
print("Recall:",metrics.recall_score(y_test, y_pred))

from sklearn.metrics import confusion_matrix
mat = confusion_matrix(ytest, yfit)
sns.heatmap(mat.T, square=True, annot=True, fmt='d', cbar=False,
            xticklabels=features,
            yticklabels=features)
plt.xlabel('true label')
plt.ylabel('predicted label')
```