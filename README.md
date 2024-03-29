# Fair-coexistence-between-LTE-LAA-WiFi-though-cross-technology-collaboration-protocol
## Summary
The technological growth combined with the exponential increase of wireless traffic are pushing the wireless community to investigate solutions to maximally exploit the available spectrum. Among the proposed solutions, the operation of Long Term Evolution (LTE) in the unlicensed spectrum (LTE-U) has attracted significant attention. Recently, the 3rd Generation Partnership Project (3GPP) announced specifications that allow LTE to transmit in the unlicensed spectrum using a Listen Before Talk (LBT) procedure, respecting this way the regulator requirements worldwide. However, the proposed standards may cause coexistence issues between LTE and legacy Wi-Fi networks. In this article, it is discussed that a fair coexistence mechanism is needed to guarantee equal channel access opportunities for the co-located networks in a technology-agnostic way, taking into account potential traffic requirements. In order to enable harmonious coexistence and fair spectrum sharing among LTE-U and Wi-Fi, an adaptive LTE-U LBT scheme is presented. This scheme uses a variable LTE transmission opportunity (TXOP) followed by a variable muting period. This way, co-located Wi-Fi networks can exploit the muting period to gain access to the wireless medium. The scheme is studied and evaluated in different compelling scenarios using a simulation platform. The results show that by configuring the LTE-U with the appropriate TXOP and muting period values, the proposed scheme can significantly improve the coexistence among LTE-U and Wi-Fi in a fair manner. Finally, a preliminary algorithm is proposed on how the optimal configuration parameters can be selected towards harmonious and fair coexistence.

## Problem definition
Recently, 3GPP announced the LTE LAA standards as part of LTE Release 13. LTE LAA defines that a CCA procedure must be performed before an LTE transmission in the unlicensed spectrum. This way, the standard can be applicable worldwide, as it respects the regional regulations in markets like Europe and Japan where a CCA procedure is mandatory.

According to LTE LAA Release 13, an eNB will be able to activate and deactivate a secondary cell operating in the unlicensed spectrum. Via this cell only DL data traffic can be sent through the Physical DL Shared Channel (PDSCH). The LTE control signals and the UL traffic will be maintained in the licensed anchor via the Physical UL Shared Channel (PUSCH). Especially for the LTE control signals whose transmission is time-critical, the licensed anchor can guarantee a safe and interference-free transmission.

Before a transmission, an eNB must perform the CCA procedure in order to sense the channel in the unlicensed spectrum. When the channel is sensed as busy, the eNB must defer its transmission and perform an exponential backoff. If the medium is sensed as idle, the eNB starts a transmission burst with a duration varying form 2 ms up to 10 ms, depending on selected channel access priority class.

On the other hand, in traditional Wi-Fi network without frame aggregation, an AP or a Station (STA) transmits only one packet after it successfully estimates the medium as idle. Such a Wi-Fi packet transmission typically lasts a few hundreds of μs. After the transmission of the packet, it has to compete again to access the medium against other co-located networks by performing a CCA procedure. In several still widely used Wi-Fi standards such as 802.11a/g frame aggregation is not supported. Even if frame aggregation is available (e.g. 802.11n/ac), often it is not used depending on the traffic type (e.g. low latency constraints).

It is clear that the transmission durations of LTE LAA and Wi-Fi are not balanced as the TXOP duration of LTE LAA is significantly longer compared to a single packet transmission of Wi-Fi. Moreover, as both networks perform an exponential backoff after they sense the channel as busy, it is possible for an LTE LAA network to gain consecutive times access to the channel forcing Wi-Fi to postpone its transmission for even longer period of time. This can lead to unfair coexistence between co-located LTE and Wi-Fi networks. Especially in the case of multiple LTE LAA networks, a co-located Wi-Fi network will be impacted drastically as it has to compete against more networks that are able to gain access to the channel for considerably longer duration.

## System description
In order to deal with this serious concern, we propose a new adaptive channel access scheme for LTE-U named mLTE-U. The purpose of the proposed scheme is to enhance the coexistence and increase the fairness among the co-located LTE-U and Wi-Fi networks. A fair coexistence scheme should offer all the available networks equal opportunities to the medium. It is important to point out the difference between fairness among different available technologies and fairness among the different coexisting networks, as it is depicted in Figure 1.

![figure1](https://user-images.githubusercontent.com/5097663/39986514-312de4be-5762-11e8-9b60-b67bf6d5939c.png)

According to the first approach (Figure 1 (a)), the wireless resources are divided among the co-located networks according to the different wireless technologies that are used. Hence, in the case of two coexisting wireless technologies such as LTE and Wi-Fi, half of the time the medium is used by LTE and half of the time is used by Wi-Fi. Such an approach is not always fair as it does not take into consideration the number of the LTE and Wi-Fi networks respectively. For instance, if there are multiple co-located Wi-Fi networks and one LTE-U network, it would not be fair to Wi-Fi to split the time that the different technologies access the channel to the half.

Regarding the second approach (Figure 1(b)), the medium is shared according to the number of the co-located networks in a technology-agnostic manner. Consequently, a coexistence mechanism that belongs in this category does not discriminate the coexisting networks based on the type of the wireless technology that they use. Instead, the distribution of the resources is done based on the number of the co-located networks and ideally based on several characteristics, such as the type and the amount of traffic that must be served.

According to the proposed scheme, LTE has to perform a CCA before a transmission. If the CCA estimates the channel as idle, then the LTE LAA eNB transmits for a variable duration called TXOP in a range of 2 ms up to 20 ms. This TXOP is followed by a variable muting period in a range of 0 ms up to 20 ms. During the muting period, the LTE-U network that has finished a transmission of a TXOP duration has to remain silent in order to give channel access opportunities to other co-located networks (e.g. Wi-Fi or another LTE-U). After the end of the muting period (or at the end of the TXOP in case of zero muting period), the eNB has to perform again a CCA procedure before a new TXOP. In this solution, the introduction of the muting period can cause problems for delay sensitive traffic. In this case, similar to LTE LAA, a primary cell operating in licensed spectrum can still be used for time sensitive transmissions. Figure 2 illustrates the proposed scheme.

![figure2](https://user-images.githubusercontent.com/5097663/39986613-7e0085da-5762-11e8-95e0-4b42a5594f1f.png)

This scheme can offer high coexistence flexibility as the mLTE-U behavior can be adapted based on various parameters, such as the number and the type of the co-located networks, the QoS requirements that a network has to serve (e.g. best effort traffic, video traffic, etc.) and the load of the different networks. For instance, when an mLTE-U network coexists with multiple Wi-Fi networks, then the proposed scheme has to be adapted so that mLTE-U transmits using a short TXOP followed by a relatively long muting period. The Wi-Fi networks can exploit this period to further gain channel access. 

Towards a fair coexistence in line with the second approach of fairness, the parameters of mLTE-U must be selected in such a way that each participating network can achieve an equal ratio of throughput, compared to the maximum throughput that it can be achieved during the standalone operation.

## Implementation details
In order to evaluate the proposed scheme, experiments have been performed using the NS3 network simulator, which is an event-based and flexible simulation platform. The simulator allows the design of scenarios in which multiple LTE networks can coexist together with multiple Wi-Fi networks in the unlicensed spectrum. The LTE and Wi-Fi networks are able to operate using the same channel and can interfere with each other.

During the experiments, the LTE has been set to operate in the 5 GHz unlicensed band. mLTE-U can transmit using a variable TXOP period, which ranges from 2 ms up to 20 ms. In addition, a muting period has been introduced to the LTE channel access scheme. This muting period ranges from 0 ms up to 20 ms and starts after the completion of a TXOP period. 

Before an mLTE-U node starts a transmission, it has to complete a CCA procedure. The CCA parameters have been configured in order to be similar to the Wi-Fi LBT Category 4 procedure. Table 1 summarizes the specific mLTE-U parameters that have been used.

![table1](https://user-images.githubusercontent.com/5097663/39986642-91d1335c-5762-11e8-9618-c457830b9488.png)

Regarding the Wi-Fi network, 802.11n mode has been selected in order to allow operation in 5 GHz unlicensed band. Additionally, frame aggregation is disabled so that we can investigate the traditional 802.11 transmission, according to which a single packet is transmitted after the channel is estimated as idle. Additionally, the network is configured to operate in SISO mode, so that the Wi-Fi operation can be comparable to other popular 802.11 standards that does not support MIMO mode such as 802.11a/g. Table 2 lists all the related parameters that have been used for the configuration of the Wi-Fi network. The common simulator parameters are presented in Table 3.

![table2](https://user-images.githubusercontent.com/5097663/39986656-9dcad082-5762-11e8-88bc-a56ba019df81.png)

![table3](https://user-images.githubusercontent.com/5097663/39986670-b0d1b77c-5762-11e8-988c-9f0fdc5063de.png)

Before the beginning of a transmission burst mLTE-U must perform a CCA procedure. This means that the medium can be sensed as idle at any time. On the other hand, LTE is a scheduled technology and the scheduling is performed by the eNB on a sub-frame level, meaning that each 1 ms the assignment of the wireless resources to the active UE can change. Hence, as every data transfer starts at the subframe boundaries, an LTE reservation signal is used after the channel is sensed as idle and until the beginning of the next subframe in order to preserve the channel and force other nodes to backoff. In the best-case but very rare scenario in which the channel is estimated as idle in the beginning of a subframe, the transmission of a reservation signal is not necessary and thus it is omitted. Contrariwise, when the channel is sensed idle immediately after the beginning of a subframe, then the reservation signal lasts for the rest of the subframe and the data transmission starts at the beginning of the next subframe. The duration of the reservation signal is deducted from the TXOP duration of the mLTE-U. For this reason, the minimum examined TXOP is 2 ms. Figure 3 illustrates the usage of the reservation signal as described above.

![figure3](https://user-images.githubusercontent.com/5097663/39986695-c1bc4a0c-5762-11e8-8ff8-0a5901ee148c.png)

## Evaluation
Several scenarios of high interest have been studied in order to evaluate the performance of the proposed scheme. As reference scenario, a topology in which one mLTE-U network coexists with one Wi-Fi network has been examined. The mLTE-U network consists of one eNB and one UE, while the Wi-Fi network consists of one AP and one STA.

Figure 4 shows the obtained DL throughput of the Wi-Fi network. The x-axis is the TXOP duration of mLTE-U in ms and the z-axis is the muting period of mLTE-U in ms. The y-axis shows the DL Wi-Fi throughput for each different combination of mLTE-U TXOP and muting period. Figure 5 presents the DL throughput of the mLTE-U network. In this diagram, the x and z axes are reversed compared to Wi-Fi. Hence the x-axis holds the muting period and the z-axis holds the TXOP duration of mLTE-U. 

![figure4-5](https://user-images.githubusercontent.com/5097663/39986712-ce79fabe-5762-11e8-9f4d-e325908369db.png)

By observing the diagrams, it can be seen that they are inverse of each other. In case of Wi-Fi, the throughput increases as the muting period of mLTE-U increases. This is logical as highest mLTE-U muting period offers more opportunities to Wi-Fi to estimate the channel as idle and start a transmission. Furthermore, the Wi-Fi throughput is inversely proportional to the mLTE-U TXOP. A shorter TXOP gives more often opportunities to Wi-Fi to compete for the medium and eventually gain access to the channel. On the contrary, the throughput of mLTE-U increases when the TXOP duration increases due to less often CCA procedure. Additionally, as it is expected, a shorter muting period offers higher throughput compared to a longer one.

In order to share the channel in a fair manner, it must be ensured that the two co-located networks can gain equal opportunities to the medium. Hence, it is expected that fair coexistence can be achieved when the mLTE-U network is configured with a TXOP and a muting period of the same duration. In Figure 6 both the mLTE-U and the Wi-Fi throughput are depicted for every pair of TXOP and muting period of the same duration.

![figure6](https://user-images.githubusercontent.com/5097663/39986731-db2f45ca-5762-11e8-9f2a-a2d996be9d52.png)

Another interesting scenario that has been investigated is a high-density scenario, where four mLTE-U networks coexist with four Wi-Fi networks. Each network consists of one base station and one end-device.

The combined throughput of Wi-Fi and of mLTE-U are shown in Figure 7 and Figure 8 respectively. 

![figure7](https://user-images.githubusercontent.com/5097663/39986742-e88d3cf4-5762-11e8-96eb-21500dea8507.png)

![figure8](https://user-images.githubusercontent.com/5097663/39986756-f2e7ae8c-5762-11e8-9a76-3dc2082c65e1.png)

Figure 7 indicates that the Wi-Fi networks are clearly impacted by the coexisting mLTE-U networks in the majority of the configurations. However, when mLTE-U is configured with short TXOP and relatively long muting period durations the combined Wi-Fi throughput is significantly improved. Due to the presence of multiple Wi-Fi networks the exploitation of these opportunities becomes even less optimal as they compete among each other to access the channel. On the other hand, the mLTE-U networks achieve a maximum combined throughput that approaches the throughput that it can be reached in the standalone operation. 

Towards a fair coexistence, the selection of TXOP and muting period must be done in a way that all the co-located networks are able to reach the 1/8 of the respective throughput of the standalone operation. Figure 9 shows the TXOP and muting period values that can offer throughput that approaches the desired values for both mLTE-U and Wi-Fi.

![figure9](https://user-images.githubusercontent.com/5097663/39986774-fbe1702c-5762-11e8-85b3-29174f814af9.png)

# Reference
For further information, you can refer to our publised article. You can cite this article as follows:

*Vasilis Maglogiannis, Dries Naudts, Adnan Shahid and Ingrid Moerman. An adaptive LTE listen-before-talk scheme towards a fair coexistence with Wi-Fi in unlicensed spectrum. Published in the Telecommunication Systems Journal, 10 January 2018. doi: 10.1007/s11235-017-0418-9*

# Contact
vasilis.maglogiannis@ugent.be
