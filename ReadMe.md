# 목차

https://www.joinc.co.kr/w/Site/Tip/SSL_cert

https://www.sysnet.pe.kr/2/0/11410#google_vignette

supersocekt
websocket4net

Server
            if (webSocketServer != null) wsStop();

            clientSession = new List<WebSocketSession>();

            sessionSyncRoot = new object();
            webSocketServer = new WebSocketServer();

            port = int.Parse(txtPort.Text);
            var bSetupOk = false;
            if (bWSS)
            {
                var config = new ServerConfig();
                config.Ip = "Any";
                //config.Port = port;
                config.Port = 443;
                config.Security = "Tls";
                config.Certificate = new CertificateConfig
                {
                    FilePath = @"d:\localhost.pfx",
                    ClientCertificateRequired = true,
                };

                bSetupOk = webSocketServer.Setup(config);
            }
            else
            {
                bSetupOk = webSocketServer.Setup(port);
            }
            if (bSetupOk)
            {
                webSocketServer.NewSessionConnected += webSocketServer_NewSessionConnected;
                webSocketServer.NewMessageReceived += webSocketServer_NewMessageReceived;
                webSocketServer.NewDataReceived += webSocketServer_NewDataReceived;
                webSocketServer.SessionClosed += webSocketServer_SessionClosed;
                ServicePointManager.ServerCertificateValidationCallback += (o, c, ch, er) => 
                true;
                webSocketServer.Start();
            }
            else
            {
                return false;
            }

            return true;

Client

            List<KeyValuePair<string, string>> keyValuePairs = new List<KeyValuePair<string, string>>();

            var username = "";
            var password = "";

            if (!string.IsNullOrEmpty(username) && !string.IsNullOrEmpty(password))
            {
                keyValuePairs = new List<KeyValuePair<string, string>>();

                var credentials = $"{username}:{password}";
                var credentialsArray = Encoding.UTF8.GetBytes(credentials);
                var base64Credential = Convert.ToBase64String(credentialsArray);
                KeyValuePair<string, string> keyValuePair = new KeyValuePair<string, string>("Authorization", $"Basic {base64Credential}");
                keyValuePairs.Add(keyValuePair);
            }

            KeyValuePair<string, string> userAgent = new KeyValuePair<string, string>("User-Agent", $"LGCharger/1.0");
            keyValuePairs.Add(userAgent);

            var connectionString = @"wss://localhost:443/NCPI000000024";
            //_webSocket = new WebSocket4Net.WebSocket(connectionString, "ocpp1.6", null, keyValuePairs, "", "",
            //                 WebSocketVersion.Rfc6455, sslProtocols: SslProtocols.Tls | SslProtocols.Tls11 | SslProtocols.Tls12);
            _webSocket = new WebSocket4Net.WebSocket(connectionString, "ocpp1.6", null, keyValuePairs, "", "",
                             WebSocketVersion.Rfc6455, sslProtocols: SslProtocols.Tls | SslProtocols.Tls11 | SslProtocols.Tls12);

            _webSocket.AutoSendPingInterval = 20;
            _webSocket.EnableAutoSendPing = true;
            _webSocket.Opened += OnWebSocketOpened;
            _webSocket.Error += OnWebSocketError;
            _webSocket.Closed += WebSocketClosed;
            _webSocket.MessageReceived += WebSocketMessageReceived;

            //System.Net.ServicePointManager.CertificatePolicy = new TrustAllCertificatePolicy();
            ServicePointManager.ServerCertificateValidationCallback+=(sender2, certificate, chain, sslPolicyErrors) => 
            true;

            //new Task(() => { _webSocket?.Open(); }).Start();

            _webSocket?.Open();



1. 제목 1 [short cut](#short-cut)
2. 제목 2
3. 제목 3
4. 제목 4
5. 제목 5
6. 제목 6
7. 제목 7
8. 제목 8
9. 제목 9

<br/><br/><br/><br/><br/><br/><br/><br/><br/><br/>
<br/><br/><br/><br/><br/><br/><br/><br/><br/><br/>
<br/><br/><br/><br/><br/><br/><br/><br/><br/><br/>
<br/><br/><br/><br/><br/><br/><br/><br/><br/><br/>
<br/><br/><br/><br/><br/><br/><br/><br/><br/><br/>
<br/><br/><br/><br/><br/><br/><br/><br/><br/><br/>
<br/><br/><br/><br/><br/><br/><br/><br/><br/><br/>
<br/><br/><br/><br/><br/><br/><br/><br/><br/><br/>
<br/><br/><br/><br/><br/><br/><br/><br/><br/><br/>
<br/><br/><br/><br/><br/><br/><br/><br/><br/><br/>

# 제목 1

Short Cut

<br/>