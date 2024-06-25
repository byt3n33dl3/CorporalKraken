FROM golang:alpine
LABEL maintainer "medoix <medoix@shivv.com> - https://medoix.com"

RUN apk add git
RUN go install github.com/pxcs/Payloads_Docker/v2@latest

RUN echo "### Dropping obfuscated eicar files ###" && \
echo -n "H4sIABva0lgAA+2XXXeaMBjH/Sje7xwXFOh6sYsEkh6RogESa2921Fl8LUygvnz6EbSzzp32YtOebc/vIuSVPAn8w5/RZNhfDuNFvbadJLWBqVf+PKjALO5cXLQrA728lpgNvaI1kKkbhm7UjQrSGgbSK1V0hlhOyNOsv6xWK/kgf8zyV/q90f6XImhqExzjEruVmpup3/TSda7KbqRSTyX33fm0d+c89OrXmfuYJENGXLzirf3AaOFGcef22u9TXpQJVbWWyt7IpFdnG3fhPQ1kpIUbxh1BiGApumOk37UFajEyaoVfbb6ZNR4CnwXCI2KihZKytk9Z4FsaCee+I2fzQMrbTFIZSku7CcSaNQO/2ULRt2IdBI85tqJdRLoz0Vv2tiO64zIWv6yd4R9wHOHOB1Lmj2IkLuG95z4E20O1nuWugvBgRS2G8X7deLNspzEK7MHtQE1s6eVu8MM02MI4i8sQfrmHx3OlavR0P/LzJZ7/SOm/VhwAZ9K+4i39ayf6r5tXddD/JejastOUeM4p492tPxQs6XkhjwXTEw95dqHLa4dKhyMWuNITXBiUS4e6grUlnXcD6Uix0YRftLni3gmpGDs0WgZWfJH3F/g9DvrP1tk7ff9P9d8wNAT6vwSg//+bUv9flP7fz/83rtCJ/g0T9H8Jjvx/2+rlVvRpq7G49Mull8fOwbs2c+Vdz3dmJD/561f+K/aGXPnrj/pLf72LsVgXI9G+D6bYWymfnz5bazibAAAAAAAAAAAAAAAAAAAAAAD4Z/kO5f7LBAAoAAA=" > /tmp/eicar-files.tar.gz.b64 && \
base64 -d /tmp/eicar-files.tar.gz.b64 > /tmp/eicar-files.tar.gz && \
rm /tmp/eicar-files.tar.gz.b64

CMD echo "### Running Malicious Tests ###" && \
echo "### Dropping Base64 encoded EICAR files ###" && \
tar xzf /tmp/eicar-files.tar.gz -C /tmp/ && \
if [ $? -eq 0 ]; then echo "--> Done"; else echo "Error: Could not extract the files"; fi && \
sleep 1 && \
for f in `ls /tmp/ | grep .b64`; do \
  srcfile="/tmp/$f"; \
  dstfile="/tmp/$(echo $f | sed -e s/.b64//g)"; \
  echo ""; \
  echo "### Dropping $dstfile ###"; \
  base64 -d $srcfile > $dstfile; \
  sleep 1; \
  if [ -s $dstfile ]; then \
    echo "--> EICAR NOT DETECTED!"; \
  else \
    echo "--> EICAR was successfully detected and removed!"; \
  fi \
done && \
echo "### Bad Network Simulation ###" && \
flightsim run
