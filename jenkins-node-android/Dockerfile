FROM infra/jenkins-node

ENV JENKINS_AGENT_NAME "android"

# switchs to root user
USER 0

# installs Android SDK
ENV ANDROID_HOME /opt/android-sdk
ENV PATH $PATH:$ANDROID_HOME/tools:$ANDROID_HOME/tools/bin:$ANDROID_HOME/platform-tools
RUN mkdir -p $ANDROID_HOME && \
    wget "https://dl.google.com/android/repository/sdk-tools-linux-3859397.zip" -P $ANDROID_HOME
RUN unzip $ANDROID_HOME/*.zip -d $ANDROID_HOME && \
    rm $ANDROID_HOME/*.zip

# installs Android's components
RUN sdkmanager tools platform-tools "platforms;android-27" "build-tools;27.0.3"

# pre-accepts Android's licenses
COPY licenses /opt/android-sdk/licenses

# switchs to default user
USER ${user}
