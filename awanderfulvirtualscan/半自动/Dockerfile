FROM ubuntu:16.04
COPY ./sources.list /etc/apt/sources.list
COPY ./acunetix_trial.sh /acunetix_trial.sh
COPY ./patch_awvs /patch_awvs
RUN chmod +x /acunetix_trial.sh/acunetix_trial.sh &&  apt-get update && apt-get install -y libxdamage1 libgtk-3-0 libasound2 libnss3 libxss1 sudo bzip2 
RUN mv /patch_awvs/patch_awvs /home/acunetix/.acunetix_trial/v_190325161/scanner/
USER acunetix
RUN /home/acunetix/.acunetix_trial/v_190325161/database/bin/pg_ctl -D /home/acunetix/.acunetix_trial/db -l logfile start
USER root