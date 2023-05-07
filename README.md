Download Link: https://assignmentchef.com/product/solved-networkprogramming-homework-2-udp-reliable-file-transfer
<br>
In this homework, you need to implement a UDP reliable file transfer protocol on the application level using 3 different timeout mechanisms.

The UDP reliable file transfer protocol includes a sender and a receiver. The sender keeps sending the content of a file to the receiver by using UDP packets. The receiver keeps receiving the content from the sender and outputs the received file content to another file. <strong>Important: the maximum size of every UDP datagram (packet) transfered is limited to 1024 Bytes.</strong>

To cope with the packet loss and re-ordering in the network, the sender and receiver should <strong>detect the packet loss events and re-ordering events</strong> (by using the timeout methods below) and deal with them (by re-transmitting lost packets).

Another important thing you should know is that <strong>the available link bandwidth between the sender and the receiver will be limited</strong> when we test your programs. Make sure that your retransmission mechanism works correctly under any link bandwidth.

Also, you have to <strong>take RTT and queuing delay into consideration</strong>. We will set RTT to a non-zero value and add variable queuing delays to packets when testing your programs.

<h2>Specification</h2>

You should implement senders and receivers using 3 different timeout methods, respectively:

<ul>

 <li>Timeout using SIGALRM</li>

 <li>Timeout using select</li>

 <li>Timeout using setsockopt</li>

</ul>

You can write as many source files as you need in this homework, and you can freely name your source files. However, after you compile your codes with Makefile, you have to make sure that <strong>there will be 6 executables generated, and named as follows</strong>:

<ul>

 <li>sender_sigalrm</li>

 <li>receiver_sigalrm</li>

 <li>sender_select</li>

 <li>receiver_select</li>

 <li>sender_sockopt</li>

 <li>receiver_sockopt</li>

</ul>

sender – UDP clientreceiver – UDP server (you can reuse)

Note: The receiver must NOT read a file locally to pretend that it has received the file from the sender.

You can output whatever information you need on the screen (stdout). We will only examine if the file sent and the file received are the same.

You can only use C or C++ in this homework.

<h3>SIGALRM</h3>

sender_sigalrm will send a file to receiver_sigalrm, and receiver_sigalrm will save the file. Due to the unreliable underlying network conditions, your sender_sigalrm and receiver_sigalrm must use <strong>SIGALRM</strong> to implement your retransmission mechanism.

The command to start the receiver:

receiver_sigalrm [save filename] [bind port]

The command to start the sender:

sender_sigalrm [send filename] [target address] [connect port]

For example, if the sender is about to send a file named a.txt to the receiver, whose IP address and port are 127.0.0.1 and 5000, and the receiver will save the file as b.txt:

<ul>

 <li>Start the receiver first:</li>

</ul>

receiver_sigalrm b.txt 5000

<ul>

 <li>Then start the sender:</li>

</ul>

sender_sigalrm a.txt 127.0.0.1 5000

<ul>

 <li>After finishing the file transfer, <strong>both </strong><strong>sender_sigalrm</strong><strong> and </strong><strong>receiver_sigalrm</strong><strong> should terminate automatically</strong>.</li>

 <li>We will test if a.txt is the same as b.txt.</li>

</ul>

Note: For the <strong>SIGALRM</strong> timeout method, you need to use <strong>siginterrupt</strong> to allow the SIGALRM signal to interrupt a system call.

<h3>select</h3>

sender_select will send a file to receiver_select, and receiver_select will save the file. Due to the unreliable underlying network conditions, your sender_select and receiver_select must use <strong>select</strong> to implement your retransmission mechanism.

The command to start the receiver:

receiver_select [save filename] [bind port]

The command to start the sender:

sender_select [send filename] [target address] [connect port]

For example, if the sender is about to send a file named a.txt to the receiver, whose IP address and port are 127.0.0.1 and 5000, and the receiver will save the file as b.txt:

<ul>

 <li>Start the receiver first:</li>

</ul>

receiver_select b.txt 5000

<ul>

 <li>Then start the sender:</li>

</ul>

sender_select a.txt 127.0.0.1 5000

<ul>

 <li>After finishing the transmission, <strong>both </strong><strong>sender_select</strong><strong> and </strong><strong>receiver_select</strong><strong> should terminate automatically</strong>.</li>

 <li>We will test if a.txt is the same as b.txt.</li>

</ul>

<h3>setsockopt</h3>

sender_sockopt will send a file to receiver_sockopt, and receiver_sockopt will save the file. Due to the unreliable underlying network conditions, your sender_sockopt and receiver_sockopt must use <strong>setsockopt</strong> to implement your retransmission mechanism.

The command to start the receiver:

receiver_sockopt [save filename] [bind port]

The command to start the sender:

sender_sockopt [send filename] [target address] [connect port]

For example, if the sender is about to send a file named a.txt to the receiver, whose IP address and port are 127.0.0.1 and 5000, and the receiver will save the file as b.txt:

<ul>

 <li>Start the receiver first:</li>

</ul>

receiver_sockopt b.txt 5000

<ul>

 <li>Then start the sender:</li>

</ul>

sender_sockopt a.txt 127.0.0.1 5000

<ul>

 <li>After finishing the transmission, you have to <strong>both </strong><strong>sender_sockopt</strong><strong> and </strong><strong>receiver_sockopt</strong><strong> should terminate automatically</strong>.</li>

 <li>We will test if a.txt is the same as b.txt.</li>

</ul>

<h2>Performance</h2>

<strong>You are free to decide whether or not to enroll in this competition to earn at most 20 bonus.</strong>

If you decide to enroll in the competition, you have to sign up the registration form, and you can only choose <strong>one retransmission mechanism that you implement (SIGALRM, select, or setsockopt)</strong> to participate in the competition.

There are two performance metrics to measure your program’s performance under unreliable underlying network conditions (packet loss, limited link bandwidth, non-zero RTT, and variable queuing delay):

<ol>

 <li>File Transfer Time (sec) (<span data-mathml="<math xmlns=&quot;http://www.w3.org/1998/Math/MathML&quot;><mrow class=&quot;MJX-TeXAtom-ORD&quot;><mi>R</mi><mn>1</mn></mrow></math>">R1R1</span>) – The shorter, the better.</li>

 <li>Total Amount of Transfered Data (Bytes) (<span data-mathml="<math xmlns=&quot;http://www.w3.org/1998/Math/MathML&quot;><mrow class=&quot;MJX-TeXAtom-ORD&quot;><mi>R</mi><mn>2</mn></mrow></math>">R2R2</span>) – The smaller, the better.</li>

</ol>

Suppose there are <span data-mathml="<math xmlns=&quot;http://www.w3.org/1998/Math/MathML&quot;><mrow class=&quot;MJX-TeXAtom-ORD&quot;><mi>M</mi></mrow></math>">MM</span> people to participate in this competition, and you are ranked <span data-mathml="<math xmlns=&quot;http://www.w3.org/1998/Math/MathML&quot;><mrow class=&quot;MJX-TeXAtom-ORD&quot;><msub><mi>r</mi><mn>1</mn></msub></mrow></math>">r1r1</span> and <span data-mathml="<math xmlns=&quot;http://www.w3.org/1998/Math/MathML&quot;><mrow class=&quot;MJX-TeXAtom-ORD&quot;><msub><mi>r</mi><mn>2</mn></msub></mrow></math>">r2r2</span> in the two performance metrics, respectively. Therefore, among total <span data-mathml="<math xmlns=&quot;http://www.w3.org/1998/Math/MathML&quot;><mrow class=&quot;MJX-TeXAtom-ORD&quot;><mi>M</mi></mrow></math>">MM</span> students, your final ranking would be <span data-mathml="<math xmlns=&quot;http://www.w3.org/1998/Math/MathML&quot;><mrow class=&quot;MJX-TeXAtom-ORD&quot;><mo stretchy=&quot;false&quot;>(</mo><msub><mi>r</mi><mn>1</mn></msub><mo>+</mo><msub><mi>r</mi><mn>2</mn></msub><mo stretchy=&quot;false&quot;>)</mo></mrow></math>">(r1+r2)(r1+r2)</span>. After that, we will sort all students with their final ranking. If you are ranked <span data-mathml="<math xmlns=&quot;http://www.w3.org/1998/Math/MathML&quot;><mrow class=&quot;MJX-TeXAtom-ORD&quot;><mi>f</mi></mrow></math>">ff</span>, you will receive <span data-mathml="<math xmlns=&quot;http://www.w3.org/1998/Math/MathML&quot;><mrow class=&quot;MJX-TeXAtom-ORD&quot;><mn>20</mn><mo>&amp;#x00D7;</mo><mo stretchy=&quot;false&quot;>(</mo><mn>1</mn><mo>&amp;#x2212;</mo><mfrac><mi>f</mi><mi>M</mi></mfrac><mo stretchy=&quot;false&quot;>)</mo></mrow></math>">20×(1−fM)20×(1−fM)</span> bonus.

For example, suppose there are <span data-mathml="<math xmlns=&quot;http://www.w3.org/1998/Math/MathML&quot;><mrow class=&quot;MJX-TeXAtom-ORD&quot;><mn>30</mn></mrow></math>">3030</span> students enrolling in the competition. Further suppose that in R1 you are ranked <span data-mathml="<math xmlns=&quot;http://www.w3.org/1998/Math/MathML&quot;><mrow class=&quot;MJX-TeXAtom-ORD&quot;><mn>15</mn></mrow></math>">1515</span> and in R2 you are ranked <span data-mathml="<math xmlns=&quot;http://www.w3.org/1998/Math/MathML&quot;><mrow class=&quot;MJX-TeXAtom-ORD&quot;><mn>3</mn></mrow></math>">33</span>. Therefore, your total ranking would be <span data-mathml="<math xmlns=&quot;http://www.w3.org/1998/Math/MathML&quot;><mrow class=&quot;MJX-TeXAtom-ORD&quot;><mn>18</mn></mrow></math>">1818</span>. Suppose that the final ranking sequence is <span data-mathml="<math xmlns=&quot;http://www.w3.org/1998/Math/MathML&quot;><mrow class=&quot;MJX-TeXAtom-ORD&quot;><mn>2</mn><mo>,</mo><mn>3</mn><mo>,</mo><mn>3</mn><mo>,</mo><mn>7</mn><mo>,</mo><mn>10</mn><mo>,</mo><mn>13</mn><mo>,</mo><mn>14</mn><mo>,</mo><mn>17</mn><mo>,</mo><mn>18</mn><mo>,</mo><mn>18</mn><mo>,</mo><mo>.</mo><mo>.</mo><mo>.</mo><mo>,</mo><mi>N</mi></mrow></math>">2,3,3,7,10,13,14,17,18,18,…,N2,3,3,7,10,13,14,17,18,18,…,N</span>. In the sequence, <span data-mathml="<math xmlns=&quot;http://www.w3.org/1998/Math/MathML&quot;><mrow class=&quot;MJX-TeXAtom-ORD&quot;><mn>18</mn></mrow></math>">1818</span> is the nineth number, so you will get <span data-mathml="<math xmlns=&quot;http://www.w3.org/1998/Math/MathML&quot;><mrow class=&quot;MJX-TeXAtom-ORD&quot;><mn>20</mn><mo>&amp;#x00D7;</mo><mo stretchy=&quot;false&quot;>(</mo><mn>1</mn><mo>&amp;#x2212;</mo><mfrac><mn>9</mn><mn>30</mn></mfrac><mo stretchy=&quot;false&quot;>)</mo><mo>=</mo><mn>14</mn></mrow></math>">20×(1−930)=1420×(1−930)=14</span> bonus.

<strong>Note that if the program you choose cannot be compiled or transfer the file correctly, you will be eliminated from the competition and get 0 bonus even though you have registered for the competition.</strong> (However, you will not get any penalty if that happens.)

<h2>Network Environment Settings</h2>

We will test if your program can work correctly under specific <strong>bi-directional packet loss rates</strong>, <strong>a non-zero RTT</strong>, and <strong>a fixed link bandwidth</strong>. We will randomly drop your packets and check whether the results are still correct.

To test your programs, you need to simulate the network scenarios (packet loss rate and packet re-ordering), and check if the file received is no different from the input.

Use the tool tc to simulate packet losses. tc is a linux built-in command line program to control the network traffic in the kernel. With tc, you can set network state parameters on a network interface card.

You should <strong>NOT</strong> use tc on the workstation (i.e. inplinux, bsd, and linux). <strong>Instead, you should do that on your own PC.</strong>

Because it requires <em>administrator permission</em> (i.e., sudo) to use tc, you can only use tc <strong>on your local pc</strong> to test if your senders and receivers work correctly when packet losses and re-ordering occur.

Of course, you still have to test your programs on the workstations to check if they can be built successfully with your Makefile, and check if they can work correctly in the ideal case (no packet loss, no link bandwidth limitation, and RTT is 0).

Refer to <a href="http://man7.org/linux/man-pages/man8/tc.8.html">man tc</a> for more information.

<h3>Add a rule to set the packet loss rate, queuing delay, link bandwidth, and re-ordering</h3>

In your linux shell, use the following command to set the <strong>packet loss rate</strong>, <strong>queuing delay</strong>, <strong>link bandwidth</strong>, and <strong>re-ordering</strong>:

sudo tc qdisc add dev &lt;Device&gt; root netem loss random &lt;Packet Loss Rate&gt; delay &lt;Delay Time&gt; &lt;Variation&gt; distribution &lt;Distribution&gt; rate &lt;Link Bandwidth&gt; reorder &lt;Percent&gt;

For example, you can add a rule on egress to set the packet loss rate to <strong>5%</strong>, set the queuing delay to between <strong>7 ms~13 ms</strong> (i.e., 10ms ± 3ms) with normal distribution, set the link bandwidth to <strong>200 kbps</strong>, and set packet re-ordering probability to <strong>25%</strong> on device “lo”.

sudo tc qdisc add dev lo root netem loss 5% delay 10ms 3ms distribution normal rate 200kbit reorder 25%

<h3>Delete all rules on a device</h3>

In your linux shell, use the following command:

sudo tc qdisc del dev &lt;Device&gt; root

For example, you can delete all rule settings on egress on the device “lo”.

sudo tc qdisc del dev lo root

Note: If there is an error message like RTNETLINK answers: File exists when you add a rule, try to delete all rules first.

<h3>Display all rules on a device</h3>

In your linux shell, use the following command:

sudo tc qdisc show dev &lt;Device&gt;

For example, you can display all rule settings on the device “lo”.

sudo tc qdisc show dev lo

<h2>Generate Test Files Randomly</h2>

You can use dd to generate a test file of a specific file size with random contents. dd is a linux built-in command line program used to convert and copy a file.

Refer to <a href="http://man7.org/linux/man-pages/man1/dd.1.html">man dd</a> for further information.

Type the following command in your linux shell to generate one file named &lt;Ouput File Name&gt; with the file size &lt;File Size&gt;:

dd if=/dev/urandom of=&lt;Output File Name&gt; bs=&lt;File Size&gt; count=1

For example, the following command generates a file named a_big_file with file size = 5MB:

dd if=/dev/urandom of=a_big_file bs=5MB count=1