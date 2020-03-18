---
description: Lista över klasser och uppräkningar som kan användas i Xamarin-program.
seo-description: Lista över klasser och uppräkningar som kan användas i Xamarin-program.
seo-title: Klasser och menyer
title: Klasser och menyer
uuid: 410d27ee-ce2b-4183-971e-39a7031d1bd5
translation-type: tm+mt
source-git-commit: df4ea2c4002611c72009cf69598cbbb74b5c15c4

---


# Klasser och menyer{#classes-and-enums}

Lista över klasser och uppräkningar som kan användas i Xamarin-program.

## Klasser {#section_E28D6156EB0F4A84AAA7749DF7D3E193}

### ADBVisitorID

```objective-c
public class ADBVisitorID : NSObject
{
    public override IntPtr ClassHandle {
        get;
    }
    public ADBVisitorID ();
    public virtual ADBMobileVisitorAuthenticationState AuthenticationState ();
    public virtual string Identifier ();
    public virtual string IdType ();
}
```

### ADBTargetLocationRequest

```objective-c
public class ADBTargetLocationRequest : NSObject
{ 
    public override IntPtr ClassHandle {
        get;
    }
    public virtual string DefaultContent {
        get;
        set;
    }
    public virtual string Name {
        get;
        set;
    }
    public virtual NSMutableDictionary Parameters {
        get;
        set;
    }

    public ADBTargetLocationRequest ();
}
```

### ADBMediaState

```objective-c
public class ADBMediaState : NSObject
{ 
    public virtual bool Ad {
        get;
        set;
    }
    public override IntPtr ClassHandle {
        get;
    }
    public virtual bool Clicked {
        get;
        set;
    }

    public virtual bool Complete {
        get;
        set;
    }
    public virtual bool EventFirstTime {
        get;
        set;
    }
    public virtual nuint EventType {
        get;
        set;
    }
    public virtual double Length {
        get;
        set;
    }
    public virtual string MediaEvent {
        get;
        set;
    }
    public virtual nuint Milestone {
        get;
        set;
    }
    public virtual string Name {
        get; 
        set; 
    } 
 
    public virtual double Offset { 
        get;
        set;
    }
    public virtual nuint OffsetMilestone {
        get;
        set;
    }
    public virtual NSDate OpenTime {
        get;
        set;
    }
    public virtual double Percent {
        get;
        set;
    }

    public virtual string PlayerName {
        get;
        set;
    }
    public virtual string Segment {
        get;
        set;
    }
    public virtual double SegmentLength {
        get;
        set;
    }
    public virtual nuint SegmentNum {
        get;
        set;
    }
    public virtual double TimePlayed {
        get;
        set;
    }
    public virtual double TimePlayedSinceTrack {
        get;
        set;
    }
    public virtual double Timestamp {
        get;
        set;
    }
    public ADBMediaState ();
}
```

### ADBMediaSettings

```objective-c
public class ADBMediaSettings : NSObject
{ 
    public virtual string Channel {
        get;
        set;
    }
    public override IntPtr ClassHandle {
        get;
    }
    public virtual nuint CompleteCloseOffsetThreshold {
        get;
        set;
    }
    public virtual string CPM {
        get;
        set;
    }
    public virtual bool IsMediaAd {
        get;
        set;
    }
    public virtual double Length {
        get;
        set;
    }
    public virtual string Milestones {
        get;
        set;
    }
    public virtual string Name {
        get;
        set;
    }
    public virtual string OffsetMilestones {
        get;
        set;
    }
    public virtual string ParentName {
        get;
        set;
    } 
    public virtual string ParentPod {
        get;
        set;
    }
    public virtual double ParentPodPosition {
        get;
        set;
    }
    public virtual string PlayerID {
        get;
        set;
    }
    public virtual string PlayerName {
        get;
        set;
    }
    public virtual bool SegmentByMilestones {
        get;
        set;
    }
    public virtual bool SegmentByOffsetMilestones {
        get;
        set;
    }
    public virtual nuint TrackSeconds {
        get;
        set;
    }
    public ADBMediaSettings (); 
}
```

### Konstanter

```objective-c
public static class Constants 
{ 
    public static NSString ADBConfigKeyCallbackDeepLink {
        get;
    }
    public static NSString ADBTargetParameterCategoryId {
        get;
    }
    public static NSString ADBTargetParameterMbox3rdPartyId {
        get;
    }
    public static NSString ADBTargetParameterMboxHost {
        get;
    }
    public static NSString ADBTargetParameterMboxPageValue {
        get;
    }
    public static NSString ADBTargetParameterMboxPc {
        get;
    }
    public static NSString ADBTargetParameterMboxSessionId {
        get;
    }
    public static NSString ADBTargetParameterOrderId {
        get;
    }
    public static NSString ADBTargetParameterOrderTotal {
        get;
    }
    public static NSString ADBTargetParameterProductPurchasedId {
        get;
    }
}
```

## Uppräkningar {#section_A78A5A305FBF4E478EAF0492E0DFD102}

### ADBMobilVisitorAuthenticationState

```objective-c
public enum ADBMobileVisitorAuthenticationState : ulong 
{ 
    Unknown, 
    Authenticated, 
    LoggedOut 
}
```

### ADBMomobilePrivacyStatus

```objective-c
public enum ADBMobilePrivacyStatus : ulong 
{ 
    OptIn = 1uL, 
    OptOut, 
    Unknown 
}
```

### ADBMobleDataEvent

```objective-c
public enum ADBMobileDataEvent : ulong 
{ 
    Lifecycle, 
    AcquisitionInstall, 
    AcquisitionLaunch, 
    DeepLink 
}
```

### ADBMobleAppExtensionType

```objective-c
public enum ADBMobileAppExtensionType : ulong 
{ 
    Regular, 
    StandAlone 
}
```
