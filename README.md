World model architecutre to learn the policies. <br>
Tested on openai gymnasium car-racing-v3 environment. <br>

World model architecture<br>

![image](https://github.com/user-attachments/assets/c312ecf1-846c-441b-ab42-8ccbbe85dd95)<br>

V(vision) is used to compress the observations to latent representation<br>
M(Memeory) is used to learn the environment dynamics<br>
C(controller) takes the input, which is a learned feature of the environment and gives action which gives max expected reward (if the learned controller is optimal or good)<br>


For V.<br>
Collected 175K states from 200 random rollouts. <br>
![image](https://github.com/user-attachments/assets/4b513d47-0f86-4def-8c5a-151c8adc30d9)

Above is decoded image from learned latent representation.<br>
it's encodes enough information to learn policy.<br>
Hope is that it increases sample effeciency<br>


Trained the agent Just using V model. and compare to the old training method (using CNN to extract the features and learn the policy)<br>
Graphs shows better reward and faster convergence using world model. (here V only)<br>


First graph, Normal method<br>
![image](https://github.com/user-attachments/assets/4e03dfc3-b13f-4626-9abd-f0e53f88bc69)

Second graph, V model only<br>
![image](https://github.com/user-attachments/assets/e055cbe9-98bd-41f7-b0ee-9276d23d513b)

we can cleary see the sample effeciency is improved<br>


Video (v model only)<br>
Couldn't do great on sharp turns <br>
Unstable, offcourse, just observation of present time-step is given <br>

![Demo](vonly.gif)

Now I trained using both V and M model. <br>

M model<br>
![image](https://github.com/user-attachments/assets/0fd73825-f700-464a-81b3-576310fead83)

Trained such that it predicts next state latent represntation.<br>
Hence this training method forces the network to learn the environment dynamcis<br>

Fig, predicted latent states by the mdn-rnn network (M - model ). (It is decoded so we can make sense seeing it)

![image](https://github.com/user-attachments/assets/eda367c2-0d0d-45ae-a2e7-21fcda1404db)

Overall architecture<br>
![image](https://github.com/user-attachments/assets/ef31d8d8-00b6-4ed9-a3b9-81c2b8e58e3e)

Used CMA-ES for training the policy here. <br>

![image](https://github.com/user-attachments/assets/d5388e73-31a5-4df3-9feb-dc317dbe41d9)

Generation Vs Reward Graph<br>
![image](https://github.com/user-attachments/assets/4df1e995-8f4e-4a63-818b-d841142f48e3)

It seems information from the hidden-state (which have past history informations of agent states) and current information that is Z (latent represntation)<br>
is enough for learning the policy (atleast for relatively simple environments)

Video,   using both V and M model<br>

![Demo](vandm.gif)



We can use the mdn-rnn to simulate entire episodes in it, itselves. which we can say we are learning the policy in the dream.<br>
when transfering back the policy in the actual environment it performs surprisingly well. <br>
I may try it in the future.<br>

Also VAE could be improved to reconstruct or give importance in those regions which are reward relavents (meaning which are important to get max rewards)<br>
too lazy to add code. may be in the future.<br>
