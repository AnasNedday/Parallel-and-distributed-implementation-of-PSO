# Parallel-and-distributed-implementation-of-PSO
## PSO: Particle Swarm Optimization
PSO is best used to find the maximum or minimum of a function defined on a multidimensional vector space. Assume we have a function F(X) that produces a real value from a vector parameter (X, Y) (such as coordinate in a plane) and X can take on virtually any value in the space. The PSO algorithm will return the parameter which produces the minimum value of the function.
### 1.PSO is a stochastic optimization technique based on the movement and intelligence of swarms.
### 2.In PSO, the concept of social interaction is used for solving a problem.
### 3.It uses a number of particles (agents) that constitute a swarm moving around in the search space, looking for the best solution.
### 4.Below is a flow diagram of PSO 

![diag.png](diag.png)
## Types of Particle Swarm Optimization
PSO algorithms can be of different types, even simple ones. The particles and velocities can be initiated in different ways. Update the Swarm and then set values for Pi and G and so on.

### Gradient Particle Swarm Optimization — We can construct gradient-based PSOs by combining the efficiency of the PSO at exploring many local minimums with the gradient-based local search algorithms. This helps us to accurately calculate a local minimum.
### Hybrid Particle Swarm Optimization — To increase and make the optimization process better, newer and more advanced types of PSO variations are being tested and used and are an ongoing field of study. A Hybrid PSO is where a normal PSO is combined with another optimization technique which helps to make it better.

## Implementing PSO with JAVA  

### Particle class
```java
public class Particle{
    private double pBestfitness;
    private double[] pBest;
    private double[] position;
    private double[] velocity;
    public double[] getpBest() {
        return pBest;
    }

    public void setpBest(double[] pBest) {
        this.pBest = pBest;
    }


    public Particle(int dim) {
        position = new double[dim];
        pBest = new double[dim];
        velocity = new double[dim];
        pBestfitness = Double.MAX_VALUE;

        Random random = new Random();
        for (int i = 0; i < dim; i++) {
            position[i] = random.nextDouble(); // Initialize position randomly in the range [0, 1]
            velocity[i] = random.nextDouble() - 0.5; // Initialize velocity randomly in the range [-0.5, 0.5]
        }
```

### getFitness
```java
 public double getfitness(double [] target) {
        double sumOfSquares = 0.0;
        for (int i = 0; i < position.length; i++) {
            sumOfSquares += Math.pow(position[i] - target[i], 2);
        }
        return Math.sqrt(sumOfSquares);

    }
```
### updatePBest() updatePosition() updateVelocity(double[] gBest)

```java
  public void updatePBest() {
        double fitness = getfitness(position);
        if (fitness < pBestfitness) {
            System.arraycopy(position, 0, pBest, 0, position.length);
            pBestfitness = fitness;
        }
    }
```
```java
 public void updatePosition() {
        for (int i = 0; i < position.length; i++) {
            position[i] += velocity[i];
        }
    }
```
  ```java 
  public void updateVelocity(double[] gBest) {
        Random random = new Random();
        for (int i = 0; i < velocity.length; i++) {
            double r1 = random.nextDouble();
            double r2 = random.nextDouble();
            velocity[i] = INERTIA_WEIGHT * velocity[i] +
                    COGNITIVE_COEFFICIENT * r1 * (pBest[i] - position[i]) +
                    SOCIAL_COEFFICIENT * r2 * (gBest[i] - position[i]);
        }
    }
    
  ```
