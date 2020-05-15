FROM alpine:3.11

RUN apk --update add --no-cache openssh bash
RUN rm -rf /var/cache/apk/*

RUN sed -i s/#PermitRootLogin.*/PermitRootLogin\ yes/ /etc/ssh/sshd_config
RUN sed -ie 's/#Port 22/Port 22/g' /etc/ssh/sshd_config
RUN sed -ri 's/#HostKey \/etc\/ssh\/ssh_host_key/HostKey \/etc\/ssh\/ssh_host_key/g' /etc/ssh/sshd_config
RUN sed -ir 's/#HostKey \/etc\/ssh\/ssh_host_rsa_key/HostKey \/etc\/ssh\/ssh_host_rsa_key/g' /etc/ssh/sshd_config
RUN sed -ir 's/#HostKey \/etc\/ssh\/ssh_host_dsa_key/HostKey \/etc\/ssh\/ssh_host_dsa_key/g' /etc/ssh/sshd_config
RUN sed -ir 's/#HostKey \/etc\/ssh\/ssh_host_ecdsa_key/HostKey \/etc\/ssh\/ssh_host_ecdsa_key/g' /etc/ssh/sshd_config
RUN sed -ir 's/#HostKey \/etc\/ssh\/ssh_host_ed25519_key/HostKey \/etc\/ssh\/ssh_host_ed25519_key/g' /etc/ssh/sshd_config

# Allow TCP forwarding
RUN sed -ir 's/AllowTcpForwarding no/AllowTcpForwarding yes/g' /etc/ssh/sshd_config 
# Allow sshd to bind any IP (0.0.0.0)
RUN sed -ir 's/GatewayPorts no/GatewayPorts yes/g' /etc/ssh/sshd_config 

COPY docker-entrypoint.sh /root/
RUN chmod +x /root/docker-entrypoint.sh
RUN mkdir /root/.ssh
RUN touch /root/.ssh/authorized_keys

EXPOSE 22
ENTRYPOINT ["/root/docker-entrypoint.sh"]