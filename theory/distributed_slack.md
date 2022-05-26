# Distributed Slack

The existence of the slack bus is a mathematical artifice. It is necessary only because the
power flow problem needs to have the same number of unknowns as equations to be solvable,
hence the selection of the slack bus in order to achieve this. If no bus is specifically selected
GridCal chooses the largest generation bus as the slack.

The problem lies in situations when the calculated slack bus power is far too large, and it
distorts the voltage results. Then a solution has been proposed; To share the slack power
among the existing generators.

$$
    P_{slack} = \sum_i^{slack} Re \{Scalc_{i} \}
$$

$$
    factors_i = \frac{S_{installed, i}}{\sum {S_{installed}}} \quad \quad \forall i \in {All \quad buses}
$$

$$
    delta_i = factors_i \cdot P_{slack}
$$

$$
    Sbus_i = Scalc_i + delta_i
$$

After a first power flow solution, the power $Scalc$ is computed and then corrected to be feed into
a second power flow run.

Where:

- $Scalc$ Power injections at the buses computed after the power flow.

- $S_{installed}$ Generation installed power per bus.
