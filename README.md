# Team-43
Distributed Deep-learning DID-acts

# Guide

This repo has been forked from Hyperledger Aries Cloudagent [link](https://github.com/hyperledger/aries-cloudagent-python) provided by British Columbia Government. 

We have created our own agents to implement a federated deep learning scenario, where participants have to present their credentials to get access to the ecosystem. These agents can be found in the /demo/runners folder. These agents connect, by default, to the BC government development of Hyperledger Indy ledger [link](http://dev.bcovrin.vonx.io).

To run the scenario:

```
git clone https://github.com/diffusioncon/Team-43

cd demo
```

## Hospital gets verified by the NHS Trust.

1) Start the NHS Trusted agent.
```
LEDGER_URL=http://dev.bcovrin.vonx.io ./run_demo nhsheadoffice
```

2) Start one of the hospitals.
```
LEDGER_URL=http://dev.bcovrin.vonx.io ./run_demo hospital1
```
3) Use NHS's invitation URL to connect the hospital to it.

4) Follow the on-screen menu to issue credentials from the NHS Trusted agent to the Hospital.

## The Researcher gets accredited by the regulatory authority.

5) Start the Coordinator.
```
LEDGER_URL=http://dev.bcovrin.vonx.io ./run_demo coordinator
```

6) Start the regulator.

```
LEDGER_URL=http://dev.bcovrin.vonx.io ./run_demo regulator

```
7) Follow the on-screen menu on the coordinator (4) to connect to the regulator.

8) Follow the on-screen menu to Issue a credential from the Regulator to the Coordinator.


## The researcher validates the hospital's identity. The hospital validates the researcher's identity. The training procedure starts.

9) Follow the on-screen menu on the Coordinator (3) to create New Invitation for the hospital.

10) Follow the on-screen menu in the hospital terminal to accept the new invitation link from the coordinator, and connect to it.

11) Follow the on-screen menu so the coordinator can check the hospital's credentials. If proof is valid, the coordinator adds this hospital to the list of the trusted connections.

12) Follow the on-screen menu to check from the hospital terminal, the coordinator's credentials. 

13) After the hospitall has been added to the coordinator's trusted list, can be start the training process by accepting the model from the coordinator, trains the model, and sends back the updated model (updated model parameters) to the coordinator. Afterwards, coordinator sends the new updated model to the next hospital to continue the training until the full training procedure has been completed.

# Inspiration

We are PhD students focused on privacy-preserving methods and techniques. Diffusion allows us to experiment, build, learn and test technologies that are too new for academia, in a short amount of time. We have experience in our team of both Identity technologies and decentralised machine learning and wanted to see how we could combine these two disciplines. The hyperledger aries secure messaging capability recently demonstrated by BC Gov at a conference seemed an interesting place to start.
What it does

Our project allows the participants to create a secure channel using DID communication. This channel can then be authenticated with relevant participants requesting credentials to ensure that the correct people are able to contribute to the learning, and reviece the trained model. Ie reduces the likelihood of a malicious learning or malicious researcher.

A trusted source as the NHS Head Office issued the credentials to the participants, and a regulatory authority granted the researcher's credentials. After the credentials validation from each side using the public DIDs, the researcher sends his model to each participant with confidence that they are legitimate. The participants train their raw data, and a secure aggregator summarizes their outputs before sent back to the researcher.

The final federated trained model defends the researcher from malicious misuses such as model poisoning attacks, and in the same time, it is protecting the privacy of the participants since their raw data never left their premises.

#How we built it

We created the secured communication channel using Hyperledger Aries. The DID of each entity is stored in a blockchain. The infrastructure is blockchain-agnostic.

We gathered mental health data relating to a survey taken by developers in 2014 [link](https://www.kaggle.com/osmi/mental-health-in-tech-survey). The dataset was federated into three batches; these three batches included in our three hospital containers, respectively. Our learning coordinator begins with an untrained model. When our learning protocol begins, the coordinator sends the untrained deep neural-network (DNN) to the first hospital, this hospital cleans its dataset, trains the DNN and sends it back to the coordinator once completed.

The coordinator then sends the updated model to the next hospital and waits for this hospital to perform the cleaning and training tasks. This process continues until each hospital has trained the model with its data. At the end of the training process, the researcher concludes with a model which trained over n batches, where n is the number of hospitals.
Challenges we ran into

We struggled with docker at times. We also planned to add a UI for visual explanation, but struggled with adapting the aries agents to a web server - this was completed. We then had issues with CORS, which we were unable to resolve in time.

# Accomplishments that we're proud of

We got to grips with the new hyperledger aries code base and cloud agent provided by the government of British Columbia. Building a complex ecosystem of issuers, verifiers and holders. We also built a federated machine learning model enabling learning to take place without data needing to leave it's original silo. We believe Hyperledger Aries can help solve the problem of secure communication between the coordinator and learners as well as enabling trust within decentralised machine learning systems.
What we learned

We explored the identity-credentials system in a complex real-world scenario, where researchers need to send their model to the participants to protect their privacy, but in the same time, they have to be protected against malicious unauthorized training.
What's next for Distributed Deep-learning DID-acts

One of the biggest unknows for us was whether the DIDComm protocol in aries could support the type of messages required to be passed between partipants in federated machine learning. The next step for this project would be to work with the Hyperledger Aries Working group to define a aries rfc for a protocol specifically designed for this use case.

# Built With

    deep-learning
    did
    docker
    federated-learning
    flask
    hyperledger-aries
    hyperledger-indy
    containerisation
    python

# Submitted to

    Diffusion 2019

# Created by

    Will Abramson
    Adam James Hall
    Pavlos Papadopoulos

