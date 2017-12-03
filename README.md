# gradient-descent
A repository to list various versions of Gradient Descent


## Gradient Descent(Simple Gradient Descent or Batch Gradient Descent)
Traditional gradient descent computes the gradients of the loss function with regards to the 
parameters for the entire training data set for a given number of epochs. 
Since we need to calculate the gradients for the whole data set, 
for just a single update this is relatively slow and even intractible for data sets
that do not fit in memory. 

## Stocastic Gradient Descent
To get around the intractibility in Batch Gradient Descent, we can use Stochastic Gradient Descent.
This is where we perform a parameter update for each training example and label. 
So we just add a loop over our training data points and calculate
the gradient with regards to each and every one. These more frequent updates with high
variance cause the objective function to fluctuate more intensely. 
This is a good thing in that it helps it jump to new and possibly better local minima. 
Where with standard gradient descent will only converge to the minimum of the
base in, where the parameters are placed in. But it also complicates convergence 
to the exact minimum since it could keep overshooting.

## Mini-Batch Gradient Descent
an improvement would be to use mini-batch gradient descent,
as it takes the best of both worlds by performing an update
for every subset of training examples that we can decide the size of. 
Training in mini-batches is usually the method of choice for 
training neural networks and we usually use the term stochastic 
gradient descent even when mini-batches are used. 

## Momemtum
The oscillations in plane old SGD make it hard to reach convergence though.
So a technique called momentum was invented that lets it
navigate along the relevant directions and softens the oscillations in the era of interactions.
All it does is it adds a fraction of the direction or
update vector of the previous step to the current step
which amplifies the speed in the correct direction.
It is just like momentum from classical physics.
When a ball is pushed down a hill, it accumulates momentum, meaning it becomes faster
and faster. In the same way our momentum term increases for dimensions whose gradients point
in the same direction, and reduces updates for dimensions whose gradients change direction.
This means 1) Faster convergence and 2) Reduced oscillations.

## Nesterov Accelerated Gradient Descent 
named after Yuri Nesterov who saw a problem with momentum.
Once we get close to our goal point the momentum is usually pretty high.
And it does not know that it should slow down which it could cause to miss the minima entirely. 
He solved this problem in a paper he released in 1983,
and we now call this strategy the Nesterov Accelerated Gradient. 
In the momentum method we compute the gradient, then make a jump
in that direction amplified by the previous momentum. In this method we 
do the same thing but in a different order. We first make a jump based on
our previous momentum, calculate the gradient, then make a correction, 
which results in an update. This more anticipatory update prevents us 
from going too fast and we are more responsive to changes. So
this idea of more dynamic learning, of adapting our updates
to the slope of our error function is a good one.

## Adaptive Gradient Descent
Adaptive gradient descent allows the learning rate to adapt based on the parameters. 
So it makes big updates for infrequent parameters and small updates for frequent parameters. 
It uses a different learning rate for every parameter at a given time step based on the past gradients
that were computed for that parameter. This means that we do not have to manually tune the learning rate. 
Its main weakness though is that the learning rate is always decreasing.
Since the accumulation of squared gradients in the denominator grows because each added
term is always positive. At some point the learning rate could get so small that the model just
stops learning entirely.

## Adaptive Delta Gradient Descent
In AdaGrad we constantly add a square root to the sum causing the
learning rate to decrease. In AdaDelta, instead of summing all the
past square roots we restrict the window of accumulated past gradients to a fixed size.
We define the sum of gradients as a decaying average of all past squared gradients
instead of just stored previous squared gradients. So the running average at a time step
depends only on the previous average and the current gradient.

Improvements so far,
- individual learning rates per parameter
- calculating momentum
- preventing decaying learning rate

## Adaptive Momentum Estimation(ADAM)
Since we are calculating learning rates for each parameter, why not also store momentum changes for
each of them separately. That is what Adam does. It stands for Adaptive moment estimation.
We calculate the first moment the mean and the 2nd moment, the un-centered variance
of the gradients respectively. Then we use those values to update the parameters just like in
AdaDelta.
