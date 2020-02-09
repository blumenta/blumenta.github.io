---
layout:     post
title:      "Curvature Flow"
subtitle:   "Using Javascript, p5.js and tf.js to unbend curves"
date:       2019-02-09 12:00:00
author:     "Alejandro Blumentals"
header-img: "../img/post-sample-img.jpg"
---

I've been learning javascript and decided to code up a little curvature flow simulation just for fun.
<iframe style="width: 800px; height: 800px; overflow: hidden;"  scrolling="no" frameborder="0" src="https://blumenta.github.io/curvature_flow/"></iframe>

The math behind it is described in [this paper](https://www.cs.cmu.edu/~kmcrane/Projects/ConformalWillmoreFlow/paper.pdf
) by Crane et al. 

# Some takeaways
* You can host javascript projects directly on github pages. 
   * Check out the deployed [demo](https://blumenta.github.io/curvature_flow/) and [repo](https://github.com/blumenta/curvature_flow).
   * You can directly embed the deployed p5.js sketch in html or jekyll markdown using an iframe
   ```html
   <iframe style="width: 800px; height: 800px; overflow: hidden;"  scrolling="no" frameborder="0" src="https://blumenta.github.io/curvature_flow/"></iframe>
   ```
* You can use vectorized array computations in javascript using tensorflow.js. You don't have all of the linear algebra functionality of numpy as far as solving linear equations goes. But you do get a Gram Schmidt decomposition, which is just what I needed here.
    ```javascript
    projectOnConstraints(f) {
        // f is an array containing the unconstrained speed
        // this function modifies that speed such that the curve remains closed.
        let e2 = [];
        let e3 = [];
        for (let i = 0; i < this.num_points; i++){
            e2[i] = this.positions[i].x;
            e3[i] = this.positions[i].y;
        }
        let x1 = tf.ones([this.num_points]);
        let x2 = tf.tensor(e2);
        let x3 = tf.tensor(e3);
        let b = tf.tensor(f);
        let A = tf.stack([x1,x2,x3]);
        let y = tf.unstack(tf.linalg.gramSchmidt(A));
        let res = tf.zerosLike(b);
        for(let i = 0; i <3; i++) {
            res = tf.add( res, tf.mul(y[i].dot(b),y[i]) )
        }
        res = tf.sub(b,res);
        return res.arraySync();
    }
```
