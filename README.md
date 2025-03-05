World model architecutre to learn the policies. 
Tested on openai gymnasium car-racing-v3 environment. 

World model architecture

![image](https://github.com/user-attachments/assets/c312ecf1-846c-441b-ab42-8ccbbe85dd95)

V(vision) is used to compress the observations to latent representation
M(Memeory) is used to learn the environment dynamcics
C(controller) take the input, which is a learned feature of the environment and gives action which gives max expected reward if the learned controller is optimal


For V.
Collected 175K states from 200 random rollouts. 
![image](https://github.com/user-attachments/assets/4b513d47-0f86-4def-8c5a-151c8adc30d9)

Above is decoded image from learned latent representation.
it's encodes enough information to learn policy.
Hope is that it increases sample effeciency


Trained the agent Just using V model. and compare to the old training method (using CNN to extract the features and learn the policy)
Graphs so better reward and faster convergence using world model. (here V only)


First graph, Normal method
![image](https://github.com/user-attachments/assets/4e03dfc3-b13f-4626-9abd-f0e53f88bc69)

Second graph, V model only
![image](https://github.com/user-attachments/assets/e055cbe9-98bd-41f7-b0ee-9276d23d513b)

we can cleary see the sample effeciency is improved



Now I trained using both V and M model. 

M model
![image](https://github.com/user-attachments/assets/0fd73825-f700-464a-81b3-576310fead83)

Overall architecture
![image](https://github.com/user-attachments/assets/ef31d8d8-00b6-4ed9-a3b9-81c2b8e58e3e)

Used CMA-ES for training the policy here. 

![image](https://github.com/user-attachments/assets/d5388e73-31a5-4df3-9feb-dc317dbe41d9)

Generation Vs Reward Graph
![image](https://github.com/user-attachments/assets/4df1e995-8f4e-4a63-818b-d841142f48e3)

Video,   using both V and M model




We can use the mdn-rnn to simulate entire episodes in it, itselves. which we can say we can learn the policy in the dream.
when transfering back the policy in the actual environment it performes surprisingly well. 
I may try it in the future.

Also VAE could be improved to reconstruct or give importance in those regions which are reward relavents (meaning which are important to get max rewards)
too lazy to add code. may be in the future.

