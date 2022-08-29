Rough work

This reverts commit 592da3f4c5ecb4ddb19bfdb208ccb05e7ab5b2b1.


//
//  Mock.swift
//  
//
//  Created by Kautilya Save on 1/5/22.
//

import Foundation
import RxSwift
import product_nameCore
import product_nameTestKit
import product_nameGraphAPI


extension Mock {
    public class UserGraphService: UserGraphServiceProtocol {
        
        public struct Stub {
            public fileprivate(set) var getUserProfileParameters: [Int] = []
            public var getUserProfileCallCount: Int {
                getUserProfileParameters.count
            }
            // Initial case starting with empty / never for Observable
            public var getUserProfileReturnValue: Observable<UserProfileGraph> = .empty()
        }
        
        public var stub = Stub()
        public init() { }
        
        // Implement the method for Stub UserProfile object isolation.
        public func getUserProfile(accountId: Int) -> Observable<UserProfileGraph> {
            stub.getUserProfileParameters.append(accountId)
            return stub.getUserProfileReturnValue
        }
    }
}
