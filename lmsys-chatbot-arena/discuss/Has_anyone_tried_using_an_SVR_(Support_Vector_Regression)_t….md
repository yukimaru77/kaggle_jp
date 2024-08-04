# Has anyone tried using an SVR (Support Vector Regression) to replace the original classification header?

**lllleeeo** *Sat Jul 20 2024 00:48:44 GMT+0900 (日本標準時)* (1 votes)

Has anyone tried using an SVR (Support Vector Regression) to replace the original classification head? I've noticed that the classification heads currently used in the public notebooks are simple linear fully connected layers, or two layers of linear heads with an activation function and dropout in the middle as someone mentioned in the comments section, and I'm wondering if using an SVR to generate predictions would perform better with the amount of data in the competition. 

I'm about to make an attempt at this but still have some concerns because then the parameters of the model are trained independently of the classification header that is ultimately used, and may blend even worse, so I'm wondering if anyone has experimented with this? We can discuss this together!😀



