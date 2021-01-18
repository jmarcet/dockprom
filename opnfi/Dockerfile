# ------------------------------------------------------------------------------
# Cargo Build Stage
# ------------------------------------------------------------------------------

FROM rust:latest as cargo-build

RUN git clone git://github.com/jrjparks/OpnFi-rs /usr/src/OpnFi-rs

WORKDIR /usr/src/OpnFi-rs

RUN cargo build --release

# ------------------------------------------------------------------------------
# Final Stage
# ------------------------------------------------------------------------------

FROM bitnami/minideb:latest

#RUN addgroup -g 1000 myapp

#RUN adduser -D -s /bin/sh -u 1000 -G myapp myapp

RUN install_packages libssl1.1 net-tools procps strace

WORKDIR /home/OpnFi

COPY --from=cargo-build /usr/src/OpnFi-rs/target/release/opnfi_device /home/OpnFi

RUN ifconfig -a
#RUN RUST_BACKTRACE=full /home/OpnFi/opnfi_device 
#-l br-lan -w pppoe-wan


#RUN chown myapp:myapp myapp

#USER myapp

#CMD ["./opnfi_device", "-h"]
#CMD ["./opnfi_device", "-l", "br-lan", "-w", "pppoe-wan"]
#CMD ["ifconfig', "-a"]
