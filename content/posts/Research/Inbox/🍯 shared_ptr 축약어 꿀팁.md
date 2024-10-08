[[📦️BASALT]]에서 알 수 있듯이
shared_ptr을 `VioEstimatorBase::Ptr`로 간략하게 쓸 수가 있따.

이는  VioEstimatorBase 클래스 안에서
`typedef std::shared_ptr<VioVisualizationData> Ptr; ` 로 맨 위에 작성해주면 할 수 있따.