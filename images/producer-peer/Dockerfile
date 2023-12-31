#Docker file for setting up the acme peer
# FROM hyperledger/fabric-peer:1.4.2
FROM hyperledger/fabric-peer:2.1

LABEL  maintainer="Mohamed Ayman"

#1. Create a folder
RUN mkdir -p /var/hyperledger/config

#2. Copy the crypto for peer crypto
COPY ./config/crypto-config/peerOrganizations/producer.supplychain.com/peers/producer /var/hyperledger/producer.supplychain.com

#3. Copy the crypto for admin crypto
COPY ./config/crypto-config/peerOrganizations/producer.supplychain.com/users /var/hyperledger/users

#4. Copy the anchor peer update tx
COPY ./config/producer-peer-update.tx /var/hyperledger/config/producer-peer-update.tx

#5. Copy the channel create tx file
COPY ./config/Prod-DistChannel.tx  /var/hyperledger/config/Prod-DistChannel.tx

#6. Copy the core YAML
COPY ./config/Producer/core.yaml /var/hyperledger/config/core.yaml

#7. Copy the bins
COPY ./bins /var/hyperledger/bins

#8. Copy the test chaincode
COPY ./nodechaincode  /var/hyperledger/nodechaincode

#9. Set the working dir
# RUN  echo "cd /var/hyperledger/bins" >> $HOME/.profile
# RUN  echo "cd /var/hyperledger/bins" >> $HOME/.bashrc
ENV  ENV="/etc/profile"
RUN  echo "cd /var/hyperledger/bins" >> /etc/profile

#10. Set the context for Admin user
# RUN echo ". /var/hyperledger/bins/set-context.sh" >> $HOME/.bashrc
RUN echo ". /var/hyperledger/bins/set-context.sh " >> /etc/profile

#11. Install the jq package - used in scripts
RUN apk update \
 && apk add jq \
 && rm -rf /var/cache/apk/*

#12. Create the package folder
RUN mkdir -p /var/hyperledger/packages

#13. Copy the gocc package tar file to the image
#COPY ./packages/gocc.1.0-1.0.tar.gz /var/hyperledger/packages/gocc.1.0-1.0.tar.gz

#14. Launch the peer
CMD peer node start
