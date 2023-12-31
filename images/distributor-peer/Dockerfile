#Docker file for setting up the budget peer
# FROM hyperledger/fabric-peer:1.4.2
FROM hyperledger/fabric-peer:2.1

LABEL  maintainer="Mohamed Ayman"

#1. Create the config subfolder
RUN mkdir -p /var/hyperledger/config

#2. Copy the crypto for peer crypto
COPY ./config/crypto-config/peerOrganizations/distributor.supplychain.com/peers/distributor /var/hyperledger/distributor.supplychain.com

#3. Copy the anchor peer update tx
COPY ./config/distributor-peer-update.tx /var/hyperledger/config/distributor-peer-update.tx

#4. Copy the crypto for admin crypto
COPY ./config/crypto-config/peerOrganizations/distributor.supplychain.com/users /var/hyperledger/users

#5. Copy the genesis file
COPY ./config/Dist-RetChannel.tx  /var/hyperledger/config/Dist-RetChannel.tx

#6. Copy the orderer YAML
COPY ./config/Distributor/core.yaml /var/hyperledger/config/core.yaml

#7. Copy the bins
COPY ./bins /var/hyperledger/bins

#8. Copy the test chaincode
COPY ./nodechaincode  /var/hyperledger/nodechaincode

#9. Set the working dir
# RUN  echo "cd /var/hyperledger/bins" >> $HOME/.profile
# RUN  echo "cd /var/hyperledger/bins" >> $HOME/.bashrc
ENV  ENV="/etc/profile"
RUN  echo "cd /var/hyperledger/bins" >> /etc/profile

#10. Set the context
# RUN echo ". /var/hyperledger/bins/set-context.sh" >> $HOME/.bashrc
RUN echo ". /var/hyperledger/bins/set-context-distributor.sh" >> /etc/profile

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
