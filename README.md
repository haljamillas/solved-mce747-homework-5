Download Link: https://assignmentchef.com/product/solved-mce747-homework-5
<br>
The purpose of this homework is to obtain a dynamic model (in symbolic form) for the Barrett WAM robot, with joints 1, 2 and 4 active and joint 3 frozen at <em>q</em><sub>3 </sub>= 0. This is done to limit the complexity of the resulting model matrices and allow you to obtain a regressor and parameters “by inspection”. This assignment will carry over into the final project.

Procedure:

<ol>

 <li>Start as if you were going to work with all four joints.</li>

 <li>Adjust the supplied code so it runs with your own transformation libraries. Look at the documentation and verify with a few easy configurations.</li>

 <li>Follow the examples discussed in class and materials posted on the course website to generate the massmatrix <em>M </em>using Matlab’s Symbolic Toolbox. Verify that the matrix is symmetric.</li>

 <li><strong>Set </strong><em>q</em><sub>3 </sub>= 0 <strong>and evaluate </strong><em>M </em><strong>to take in this value. Then remove the third row and the third column to obtain a 3-by-3 matrix</strong>.</li>

 <li>Obtain the Coriolis matrix symbolically using <em>M </em>and the gravity vector. Remember to ignore the gravity vector component corresponding to joint 3.</li>

 <li>Verify the skew-symmetry property by symbolic differentiation of <em>M</em>.</li>

 <li>Inspect each one of the 6 distinct entries of <em>M </em>to identify Θ parameters. Suggested procedure:

  <ul>

   <li>Display <em>M</em>(1<em>,</em>1) and copy-paste its constant portion, assigning it to Θ1. Remove this parameter from <em>M</em>(1<em>,</em>1) to obtain a shorter expression.</li>

   <li>Look at the kinds of terms showing in <em>M</em>(1<em>,</em>1), for instance cos(2<em>q</em>2 + <em>q</em>4)<em>, </em>sin(<em>q</em>2), etc. Use subs as follows:</li>

  </ul></li>

</ol>

&gt;&gt; syms c24; term=subs(M(1,1),cos(2*q2+q4), c24); coeff=diff(term,c24)

This puts a placeholder c24 and allows you to extract its coefficient by taking the partial derivative. This coefficient will be a Θ parameter.

<ul>

 <li>Shorten <em>M</em>(1<em>,</em>1) further by removing the identified coefficient times the corresponding trig function.</li>

 <li>This procedure will eventually cover all entries of <em>M</em>, but it will take a few hours of focused work.</li>

</ul>

<ol start="8">

 <li>Without scanning for linearly-dependent Θ parameters, the instructor found that 19 parameters werenecessary to describe <em>M</em>. (there was one obviously repeated parameter).</li>

 <li>Identify a few more parameters for the gravity vector. In all, the instructor found 25 parameters. Howmany fundamental parameters (individual masses, lengths, etc) were initially present?</li>

 <li>Obtain the Coriolis matrix in Θ form.</li>

 <li>Verify that the parameterization works by evaluating <em>Mq</em>¨+<em>Cq</em>˙+<em>g </em>with the non-parameterized matrices and the Θ forms, as done in class.</li>

 <li>Obtain the regressor <em>Y </em>(<em>q,q,</em>˙ <em>q</em>¨) by partial differentiation of <em>Mq</em>¨+<em>Cq</em>˙ +<em>g </em>in parameter form, as done in class.</li>

 <li>Code a state derivative function for use in Simulink that returns the state derivatives of the robot dynamics. Numerical values are involved at this point, not earlier. It is recommended to use the parameter form of the dynamic matrices in this code (it is more compact). The state derivative function can receive the numerical Θ vector as a parameter from a Simulink constant block.</li>

 <li>Simulate the joint motion that results when the applied torques are all equal to sin(<em>t</em>). Simulate for 5 seconds.</li>

 <li>Extra points question: setting all initial angles to zero (robot upright) and all initial velocities to zeroresults in a nonzero initial acceleration for joint 1. How is this possible? – Explain fully.</li>

</ol>