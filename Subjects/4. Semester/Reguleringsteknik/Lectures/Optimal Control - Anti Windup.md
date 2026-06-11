Anti windup is a **MUST** when working with [[Subjects/4. Semester/Reguleringsteknik/Lectures/Integral Control|Integral Control]] as accumulation over time can lead to unwanted behavior. Anti windup introduces a saturation point, where the data cannot accumulate anymore.
![[Pasted image 20260611154131.png]]

This is seen by the anti windup blocks on the black and orange entry points (so from $F\hat x$).

To choose how the system behaves while _in saturation_ we can introduce a _saturation matrix_ $M$
![[Pasted image 20260611154252.png]]

Since $M$ finds the difference between $F\hat x$ before saturation control and after saturation control, the difference will be 0, until the system reaches saturation wher